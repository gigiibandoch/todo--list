<script setup>
import { computed, ref } from 'vue'
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
const filtro = ref('')
const tarefasFiltradas = computed(() => {
  if(filtro.value.trim().length > 0) {
    return tarefas.value.filter( item => item.tarefa.includes(filtro.value));
  }
  else {
    return tarefas.value;
  }
})
function ordenarArray() {
  tarefas.value.sort((a, b) => a.tarefa.localeCompare(b.tarefa));
}
</script>

<template>
<div class="container">
<h1>Lista de Tarefas</h1>
<input type="text" v-model="novaTarefa" placeholder="Adicionar nova tarefa">
<button @click="addTarefa">{{ posicaoAlterada == -1 ? "Adicionar" : "Salvar" }}</button>

<ul>
<li v-for="item in tarefasFiltradas" :key="item.id"  :class="{ concluida: item.status === 'concluida' }"> >
{{ item.tarefa }}
<button @click="delTarefa(item.id)" >X</button>
<button @click="editTarefa(item.id)" >Editar</button>
</li>
</ul>
<input type="text" placeholder="Filtrar tarefa" v-model="filtro">
<button @click="ordenarArray" >Ordenar</button>
</div>
</template>

<style scoped>
div h1 {
  color: rgb(235, 156, 255);
}
div {
  align-items: center;
}
div button {
  background-color: rgb(235, 156, 255);
  border-radius: 10px;
  color: rgb(0, 0, 0);
  padding: 4px 20px;
  margin: 20px;
  font-size: 0.8rem;
}
div input::placeholder {
  color: rgb(46, 46, 46);
}
.concluida {
  text-decoration: line-through;
  color:  rgb(235, 156, 255);
}
</style>