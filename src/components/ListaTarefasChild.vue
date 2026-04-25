<script setup>
import TestItem from './TestItem.vue'

defineProps(['tarefas'])
defineEmits(['status', 'editar', 'excluir'])
</script>

<template>
  <ul>
    <TestItem
      v-for="tarefa in tarefas"
      :key="tarefa.id"
      :tarefa="tarefa"
      @status="$emit('status', $event)"
      @editar="$emit('editar', $event)"
      @excluir="$emit('excluir', $event)"
    />
  </ul>
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