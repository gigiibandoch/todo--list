<script setup>
defineProps(['tarefa'])
const emit = defineEmits(['status', 'excluir', 'editar'])

import ButtonChild from './ButtonChild.vue';
</script>

<template>
  <li :class="{ concluida: tarefa.status === 'concluida' }">
    <span @click="emit('status', tarefa)">
      {{ tarefa.tarefa }}
    </span>
    <ButtonChild @click="emit('editar', tarefa.id)">Editar</ButtonChild>
    <ButtonChild @click="emit('excluir', tarefa)">X</ButtonChild>
  </li>
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