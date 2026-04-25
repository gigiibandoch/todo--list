<script setup>
const emit = defineEmits(['ordenar', 'recuperar'])
import ButtonChild from './ButtonChild.vue'
</script>

<template>
  <ButtonChild @clique="emit('ordenar')">
    Ordenar
  </ButtonChild>

  <ButtonChild @clique="emit('recuperar')">
    Recuperar
  </ButtonChild>
</template>
<style scoped>
div h1 {
  color: rgb(235, 156, 255);
} 
div button {
  background-color: rgb(235, 156, 255);
  border-radius: 10px;
  color: rgb(0, 0, 0);
  padding: 4px 20px;
  margin: 5px;
  font-size: 0.8rem;
}
div input::placeholder {
  color: rgb(46, 46, 46);
}
.concluida {
  text-decoration: line-through;
  color: rgb(235, 156, 255);
}
</style>