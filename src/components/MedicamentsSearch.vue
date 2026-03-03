<script setup>
import { ref } from 'vue';
const libelle = ref(''); // c’est une variable réactive
const emit = defineEmits(['eventSearch']); // définir l'événement eventAdd
</script>

<template>
  <h3>Recherche de Médicament :</h3>
  <form @submit.prevent="$emit('eventSearch', libelle)">
    <input v-model="libelle" type="text" placeholder="Nom de Médicament" />
    <button type="submit">Rechercher</button>
  </form>
</template>
