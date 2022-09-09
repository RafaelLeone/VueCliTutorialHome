<template>
  <div id="home">
    <nav class="orange darken-2">
      <img alt="Vue logo" src="../assets/logo.png" width="64" />
      <div class="nav-wrapper"></div>
    </nav>
    <div>
      <button class="btn" @click="mostrarForm" v-show="exibir.lista">
        Adicionar
      </button>
    </div>
    <div v-show="exibir.lista">
      <TarefaList msg="Welcome to Your Vue.js Home" :tasks="listaDeTarefas" />
    </div>
    <TarefaForm @salvarClick="recebiSalvar" :titulo="forms.title"></TarefaForm>
  </div>
</template>

<script>
import TasksApi from '../TasksApi.js'
import TarefaList from '../components/TarefaList.vue'
import TarefaForm from '../components/TarefaForm.vue'

export default {
  name: 'HoMe',
  components: {
    TarefaList,
    TarefaForm,
  },
  data: () => {
    return {
      exibir: {
        lista: true,
        forms: false,
      },
      forms: {
        title: 'Cadastrar nova tarefa',
      },
      listaDeTarefas: ['A', 'B', 'C'],
    }
  },
  methods: {
    listarTarefas() {
      TasksApi.getTasks((data) => {
        this.listaDeTarefas = data
      })
    },
    mostrarForm() {
      this.exibir.forms = true
      this.exibir.lista = false
    },
    recebiSalvar(novaTarefa) {
      TasksApi.createTask(novaTarefa, () => {
        this.listarTarefas()
        this.exibir.forms = false
        this.exibir.lista = true
      })
    },
  },
  created() {
    this.listarTarefas()
  },
}
</script>

<style></style>
