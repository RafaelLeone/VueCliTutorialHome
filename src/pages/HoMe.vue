<template>
  <div id="home">
    <nav class="orange darken-2">
      <img alt="Vue logo" src="../assets/logo.png" width="64" />
      <div class="nav-wrapper"></div>
    </nav>
    <div>
      <button @click="mostrarForm">Adicionar</button>
    </div>
    <div v-show="exibir.lista">
      <TarefaList msg="Welcome to Your Vue.js Home" :tasks="listaDeTarefas" />
    </div>

    <div v-show="exibir.forms">
      <h3>Cadastrar nova tarefa</h3>
      <input
        type="text"
        name="title"
        id="title"
        placeholder="Digite o nome da tarefa"
        v-model="forms.title"
      />
      <button class="btn" @click="salvarTarefa">Salvar Tarefa</button>
      <button @click="cancelarTarefa">Cancelar</button>
    </div>
  </div>
</template>

<script>
import TasksApi from '../TasksApi.js'
import TarefaList from '../components/TarefaList.vue'

export default {
  name: 'HoMe',
  components: {
    TarefaList,
  },
  data: () => {
    return {
      exibir: {
        lista: true,
        forms: false,
      },
      forms: {
        title: '',
      },
      listaDeTarefas: ['A', 'B', 'C'],
    }
  },
  methods: {
    mostrarForm() {
      this.exibir.forms = true
      this.exibir.lista = false
    },
    cancelarTarefa() {
      this.exibir.forms = false
      this.exibir.lista = true
    },
    salvarTarefa() {
      console.log('sdsd')
      this.exibir.forms = false
      this.exibir.lista = true
      const novaTarefa = {
        title: this.forms.title,
        date: new Date().toLocaleDateString('pt'),
      }
      TasksApi.createTask(novaTarefa, (resp) => {
        console.log('deu certo', resp)
      })
    },
  },
  created() {
    TasksApi.getTasks((data) => {
      this.listaDeTarefas = data
    })
  },
}
</script>

<style></style>
