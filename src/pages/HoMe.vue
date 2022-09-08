<template>
  <div id="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <TarefaList msg="Welcome to Your Vue.js Home" :tasks="listaDeTarefas" />
    <p>{{ listaDeTarefas }}</p>
  </div>
</template>

<script>
import axios from "axios";
import TarefaList from "../components/TarefaList.vue";

export default {
  name: "HoMe",
  components: {
    TarefaList,
  },
  data: () => {
    return {
      listaDeTarefas: ["A", "B", "C"],
    };
  },
  created() {
    console.log("terminei de carregar a página");
    axios.get("http://localhost:3000/tasks/").then((response) => {
      console.log(response.data);
      this.listaDeTarefas = response.data;
    });
  },
};
</script>

<style>
#home {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
