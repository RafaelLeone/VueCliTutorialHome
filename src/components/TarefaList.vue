<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ul
      style="display: flex; flex-direction: column-reverse"
      class="collection"
    >
      <li class="collection-item" v-for="t in tasks" :key="t.id">
        <h5>
          {{ t.titulo }}
          <span class="task-badge right-align">{{ t.project }}</span>
        </h5>
        <button class="btn btn-small" @click="editarClick(t.id)">EDIT</button>
        <button class="btn btn-small" @click="deleteClick(t.id)">DELETE</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TarefaList',
  props: {
    msg: String,
    tasks: Array,
  },
  methods: {
    editarClick(tarefaId) {
      this.$emit('editarClick', tarefaId)
    },
    deleteClick(tarefaId) {
      this.$emit('deleteClick', tarefaId)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.task-badge {
  background-color: #929292;
  color: white;
  padding: 6px;
  border-radius: 6px;
  font-size: 0.8rem;
  vertical-align: middle;
}
</style>
