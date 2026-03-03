<script setup>
defineProps(['med']);
defineEmits(['eventDelete', 'eventIncrement', 'eventDecrement']);
</script>

<template>
  <li>
    {{ med.denomination }} - Stock: {{ med.qte }} - Forme:
    {{ med.formepharmaceutique }}
    <img
      v-if="med.photo"
      :src="'https://apipharmacie.pecatte.fr/images/' + med.photo"
      alt="image du medicament"
      width="150"
    />
    <button @click="$emit('eventIncrement', med)">+1</button>
    <button @click="$emit('eventDecrement', med)">-1</button>
    <button @click="$emit('eventDelete', med.id)">Delete</button>
  </li>
</template>
