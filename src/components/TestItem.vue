<script setup>
defineProps(['tarefa'])
const emit = defineEmits(['status', 'excluir', 'editar'])
</script>

<template>
  <li :class="{ concluida: tarefa.status === 'concluida' }">
    <span @click="emit('status', tarefa)">
      {{ tarefa.tarefa }}
    </span>
    <button @click="emit('editar', tarefa.id)">Editar</button>
    <button @click="emit('excluir', tarefa)">X</button>
  </li>
</template>

<style scoped>
button {
  background-color: rgb(235, 156, 255);
  border-radius: 10px;
  color: rgb(0, 0, 0);
  padding: 4px 20px;
  margin: 5px;
  font-size: 0.8rem;
}
</style>