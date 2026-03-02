<script setup>
defineProps(['med']); // reçoit le médicament
defineEmits(['eventDelete']);
</script>

<template>
  <li>
    <button @click="$emit('eventDelete', med.id)">
      Delete
    </button>
  </li>
</template>
