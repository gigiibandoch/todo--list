<script setup>
import { ref } from 'vue'
const tarefas = ref([
{
id: 1,
tarefa: 'Tarefa 1',
status: 'concluida'
},
{
id: 2,
tarefa: 'Tarefa 2',
status: 'concluida',
},
{
id: 3,
tarefa: 'Tarefa 3',
status: 'pendente'
},
{
id: 4,
tarefa: 'Tarefa 4',
status: 'pendente'
}
])

const novaTarefa = ref('')
const posicaoAlterada = ref(-1)

function addTarefa() {
  if (posicaoAlterada.value == -1) {
    let novoID = Math.max(...tarefas.value.map(item => item.id)) + 1;
    tarefas.value.push({ id: novoID, tarefa: novaTarefa.value, status: 'pendente'});
  }
  else {
    tarefas.value[posicaoAlterada.value].tarefa = novaTarefa.value;
  }
  novaTarefa.value = '';
  posicaoAlterada.value = -1;
}

function delTarefa(item) {
  let posicao = tarefas.value.indexOf(item);
  tarefas.value.splice(posicao, 1);
}

function editTarefa(idItem) {
  posicaoAlterada.value = tarefas.value.findIndex(item => item.id == idItem);
  novaTarefa.value = tarefas.value[posicaoAlterada.value].tarefa;
}
</script>

<template>
<div class="container">
<h1>Lista de Tarefas</h1>
<input type="text" v-model="novaTarefa">
<button @click="addTarefa">{{ posicaoAlterada == -1 ? "Adicionar" : "Salvar" }}</button>
<ul>
<li v-for="item in tarefas" :key="item.id">
{{ item.tarefa }}
<button @click="delTarefa(item.id)" >X</button>
<button @click="editTarefa(item.id)" >Editar</button>
</li>
</ul>
</div>
</template>

<style scoped>
</style>