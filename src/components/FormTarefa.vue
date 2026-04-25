<script setup>
const props = defineProps(['novaTarefa', 'modoEdicao'])
const emit = defineEmits(['inputTarefa', 'salvar'])

import ButtonChild from './ButtonChild.vue'
</script>

<template>
  <input
    type="text"
    :value="props.novaTarefa"
    @input="emit('inputTarefa', $event.target.value)"
    placeholder="Adicionar nova tarefa"
  />

  <ButtonChild @clique="emit('salvar')">
    {{ props.modoEdicao ? "Salvar" : "Adicionar" }}
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