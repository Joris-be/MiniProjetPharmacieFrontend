<script setup>
import { ref } from 'vue';
const denomination = ref(''); // le nom que l’utilisateur tape
const formepharmaceutique = ref('Comprimé'); // valeur par défaut
const qte = ref(1); // quantité par défaut
const photo = ref(''); // URL ou nom de la photo

const emit = defineEmits(['eventAdd']);

function submitForm() {
  // Crée un objet médicament complet
  const med = {
    denomination: denomination.value,
    formepharmaceutique: formepharmaceutique.value,
    qte: qte.value,
    photo: photo.value,
  };

  emit('eventAdd', med); // envoie l’objet au parent
  denomination.value = '';
  formepharmaceutique.value = '';
  qte.value = 1;
  photo.value = '';
}
</script>

<template>
  <form @submit.prevent="submitForm">
    <input
      v-model="denomination"
      type="text"
      placeholder="Nom du médicament"
      required
    />
    <input
      v-model="formepharmaceutique"
      type="text"
      placeholder="Forme pharmaceutique"
      required
    />
    <input
      v-model.number="qte"
      type="number"
      placeholder="Quantité"
      min="0"
      required
    />
    <input v-model="photo" type="text" placeholder="Nom ou URL de la photo" />

    <button type="submit">Ajouter</button>
  </form>
</template>
