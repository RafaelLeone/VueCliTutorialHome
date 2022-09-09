<template>
  <div>
    <h3>{{ titulo }}</h3>
    <input
      type="text"
      name="title"
      id="title"
      placeholder="Digite o nome da tarefa"
      v-model="forms.title"
    />
    <button class="btn" @click="salvarTarefa">Salvar Tarefa</button>
  </div>
</template>

<script>
export default {
  props: ['titulo'],
  data: () => {
    return {
      forms: {
        title: '',
        project: '',
      },
    }
  },

  methods: {
    salvarTarefa() {
      const novaTarefa = {
        title: this.forms.title,
        project: this.forms.project,
        date: new Date().toLocaleDateString('pt'),
      }
      this.$emit('salvarClick', novaTarefa)
    },
  },
}
</script>
