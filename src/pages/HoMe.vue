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
      <TarefaList
        @editarClick="recebiEditar"
        @deleteClick="recebiDeletar"
        msg="Welcome to Your Vue.js Home"
        :tasks="listaDeTarefas"
      />
    </div>
    <div v-show="exibir.forms">
      <TarefaForm
        :id="form.id"
        :btn="form.btn"
        @salvarClick="recebiSalvar"
        @alterarClick="recebiAlterar"
        :titulo="form.titulo"
        :title="form.title"
        :project="form.project"
      ></TarefaForm>
    </div>
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
      form: {
        id: 0,
        titulo: '',
        project: '',
        btn: 'Adicionar',
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
    recebiAlterar(tarefa) {
      TasksApi.updateTask(tarefa, () => {
        this.listarTarefas()
        this.exibir.forms = false
        this.exibir.lista = true
      })
    },
    recebiEditar(tarefaId) {
      console.log('chegou a ' + tarefaId)
      this.form.btn = 'Alterar'
      this.form.title = 'Alterar tarefa'
      TasksApi.getTask(tarefaId, (task) => {
        this.form.id = task.id
        this.form.titulo = task.titulo
        this.form.project = task.project
        this.exibir.forms = true
        this.exibir.lista = false
      })
    },
    recebiDeletar(tarefaId) {
      console.log('cheguei', tarefaId)
      TasksApi.deleteTask(tarefaId, () => {
        this.listarTarefas()
      })
    },
  },
  created() {
    this.listarTarefas()
  },
}
</script>

<style></style>
