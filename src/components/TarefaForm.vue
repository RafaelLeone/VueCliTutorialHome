<template>
  <div>
    <h3>{{ title }}</h3>
    <input
      type="text"
      name="titulo"
      :value="titulo"
      @input="form.titulo = $event.target.value"
      id="titulo"
      placeholder="Digite o nome da tarefa"
    />
    <input
      type="text"
      name="project"
      id="project"
      placeholder="Digite o nome da tag"
      :value="project"
      @input="form.project = $event.target.value"
    />
    <button class="btn" @click="salvarTarefa">{{ btn }}</button>
  </div>
</template>

<script>
export default {
  props: ['titulo', 'title', 'project', 'btn', 'id'],
  data: () => {
    return {
      form: {
        titulo: '',
        project: '',
      },
    }
  },

  methods: {
    salvarTarefa() {
      const novaTarefa = {
        titulo: this.form.titulo,
        project: this.form.project,
      }
      if (this.btn == 'Adicionar') {
        novaTarefa.date = new Date().toLocaleDateString('pt')
        this.$emit('salvarClick', novaTarefa)
      } else {
        novaTarefa.id = this.id
        this.$emit('alterarClick', novaTarefa)
      }
    },
  },
}
</script>
