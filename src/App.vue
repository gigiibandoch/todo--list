<script setup>
import { computed, ref } from 'vue'
import TestItem from './components/TestItem.vue'
import ButtonChild from './components/ButtonChild.vue'
import AcoesTarefa from './components/AcoesTarefa.vue'
import FormTarefa from './components/FormTarefa.vue'
import FiltroTarefa from './components/FiltroTarefa.vue'
import ListaTarefasChild from './components/ListaTarefasChild.vue'
import { listaTarefas } from './data/tarefas'
const tarefas = ref(listaTarefas)


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
  tarefas.value.sort((a, b) => a.tarefa.localeCompare(b.tarefa, 'pt-BR'));
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


const editando = ref(false)

function receberInput(valor) {
  novaTarefa.value = valor
}

function atualizarFiltro(valor) {
  filtro.value = valor
}
</script>

<template>
  <div class="container">
    <h1>Lista de Tarefas</h1>

    <FormTarefa
      :novaTarefa="novaTarefa"
      :modoEdicao="editando"
      @inputTarefa="receberInput"
      @salvar="addTarefa"
    />

    <ListaTarefasChild
      :tarefas="tarefasFiltradas"
      @status="alterarStatus"
      @editar="editTarefa"
      @excluir="delTarefa"
    />

    <FiltroTarefa
      :filtro="filtro"
      @filtrar="atualizarFiltro"
    />

    <AcoesTarefa
      @ordenar="ordenarArray"
      @recuperar="recuperarTarefas"
    />

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