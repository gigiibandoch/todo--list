<script setup>
import { computed, ref } from 'vue'

const tarefas = ref([
  { id: 1, tarefa: 'Tarefa 1', status: 'concluida' },
  { id: 2, tarefa: 'Tarefa 2', status: 'concluida' },
  { id: 3, tarefa: 'Tarefa 3', status: 'pendente' },
  { id: 4, tarefa: 'Tarefa 4', status: 'pendente' }
])

const novaTarefa = ref('')
const posicaoAlterada = ref(-1)
const tarefasRemovidas = ref([])

function addTarefa() {
  if (posicaoAlterada.value == -1) {
    let novoID = Math.max(...tarefas.value.map(item => item.id)) + 1
    tarefas.value.push({ id: novoID, tarefa: novaTarefa.value, status: 'pendente'})
  }
   else {
    tarefas.value[posicaoAlterada.value].tarefa = novaTarefa.value
  }

  novaTarefa.value = ''
  posicaoAlterada.value = -1
}

function delTarefa(item) {
  let posicao = tarefas.value.indexOf(item)
  tarefasRemovidas.value.push(item)
  tarefas.value.splice(posicao, 1)
}

function editTarefa(idItem) {
  posicaoAlterada.value = tarefas.value.findIndex(item => item.id == idItem)
  novaTarefa.value = tarefas.value[posicaoAlterada.value].tarefa
}

function alterarStatus(item) {
  item.status = item.status === 'pendente' ? 'concluida' : 'pendente'
}

const filtro = ref('')

const tarefasFiltradas = computed(() => {
  if (filtro.value.trim().length > 0) {
    return tarefas.value.filter(item =>
      item.tarefa.toLowerCase().includes(filtro.value.toLowerCase())
    )
  } else {
    return tarefas.value
  }
})

function ordenarArray() {
  tarefas.value.sort((a, b) => a.tarefa.localeCompare(b.tarefa))
}

const concluidas = computed(() => {
  return tarefas.value.filter(item => item.status === 'concluida').length
})

const pendentes = computed(() => {
  return tarefas.value.filter(item => item.status === 'pendente').length
})

function recuperarTarefas() {
  if (tarefasRemovidas.value.length === 0) return
  tarefas.value.push(...tarefasRemovidas.value)
  tarefasRemovidas.value = []
}

</script>

<template>
  <div class="container">
    <h1>Lista de Tarefas</h1>
    <input type="text" v-model="novaTarefa" placeholder="Adicionar nova tarefa"/>
    <button @click="addTarefa">
      {{ posicaoAlterada == -1 ? "Adicionar" : "Salvar" }}
    </button>
    <ul>
      <li v-for="item in tarefasFiltradas" :key="item.id" :class="{ concluida: item.status === 'concluida' }">
        <span @click="alterarStatus(item)">
          {{ item.tarefa }}
        </span>
        <button @click="editTarefa(item.id)">Editar</button>
        <button @click="delTarefa(item)">X</button>
      </li>
    </ul>
    <input type="text" placeholder="Filtrar tarefa" v-model="filtro"
    />
    <button @click="ordenarArray">Ordenar</button>
    <button @click="recuperarTarefas">Recuperar</button>
    <p>Pendentes: {{ pendentes }}</p>
    <p>Concluídas: {{ concluidas }}</p>
  </div>
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