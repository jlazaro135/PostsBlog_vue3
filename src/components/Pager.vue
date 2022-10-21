<script setup>
defineProps(['inicio', 'fin', 'maxLength'])
const emit = defineEmits(['next', 'prev'])
</script>

<template>
<div class="btn-group" role="group" aria-label="Basic example">
  <button type="button" 
  @click="emit('prev')" 
  class="btn btn-outline-primary"
  :disabled="inicio <= 0"
  >Anterior</button>
  <button type="button" 
  @click="emit('next')" 
  class="btn btn-outline-primary"
  :disabled="fin >= maxLength"
  >Siguiente</button>
</div>
</template>

<style scoped>
</style>