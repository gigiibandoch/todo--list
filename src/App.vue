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

function addTarefa(tarefas) {
  let novoID = Math.max(...listaCompras.map(p => p.id)) + 1;
  tarefas.push({ id: novoID, nome: 'Tarefa 5', status: 'pendente'});
}
</script>

<template>
<div class="container">
<h1>Lista de Tarefas</h1>
<input type="text" v-model="novaID">
<button @click="addTarefa">Adicionar</button>
<ul>
<li v-for="item in tarefas" :key="item.id">
{{ item.tarefa }}
</li>
</ul>
</div>
</template>

<style scoped>
</style>