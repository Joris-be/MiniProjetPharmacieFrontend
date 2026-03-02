<script setup>
import { reactive, onMounted } from 'vue';
import MedicamentsForm from './MedicamentsForm.vue';
import MedicamentsListItem from './MedicamentsListItem.vue';

const listeMedicaments = reactive([]);
const url = 'https://apipharmacie.pecatte.fr/api/22/medicaments';

function getMedicaments() {
  const fetchOptions = { method: 'GET' };
  listeMedicaments.length = 0;
  fetch(url, fetchOptions)
    .then((response) => response.json())
    .then((dataJSON) => {
      dataJSON.forEach((med) => listeMedicaments.push(med));
    })
    .catch((error) => {
      console.log(error);
    });
}
onMounted(() => {
  getMedicaments();
});

function handlerAddMedicament(med) {
  let myHeaders = new Headers();
  myHeaders.append('Content-Type', 'application/json');
  const fetchOptions = {
    method: 'POST',
    headers: myHeaders,
    body: JSON.stringify(med), // ici on envoie l'objet JSON
  };
  fetch(url, fetchOptions)
    .then((response) => response.json())
    .then((dataJSON) => {
      listeMedicaments.push(dataJSON);
    })
    .catch((error) => {
      console.log(error);
    });
}

function handlerDeleteMedicament(med) {
  const fetchOptions = {
    method: 'DELETE',
  };
  fetch(url, fetchOptions)
    .then((response) => response.json())
    .then((dataJSON) => {
      getMedicaments();
    })
    .catch((error) => {
      console.log(error);
    });
}
</script>

<template>
  <h3>Liste des médicaments</h3>
  <MedicamentsForm @eventAdd="handlerAddMedicament"></MedicamentsForm>
  <div class="medicaments-container">
    <ul>
      <li v-for="med in listeMedicaments" :key="med.reference">
        {{ med.denomination }} - Stock: {{ med.qte }} - Forme:
        {{ med.formepharmaceutique }}
        <img
          v-if="med.photo"
          :src="'https://apipharmacie.pecatte.fr/images/' + med.photo"
          alt="image du medicament"
          width="150"
        />
      </li>
      <MedicamentsListItem
        v-for="med in listeMedicaments"
        :key="med.id"
        :med="med"
        @eventDelete="handlerDeleteMedicament"
      />
    </ul>
  </div>
</template>
