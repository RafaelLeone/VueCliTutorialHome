<template>
  <div id="home">
    <nav class="orange darken-2">
      <div class="nav-wrapper"></div>
    </nav>
    <img alt="Vue logo" src="../assets/logo.png" />
    <TarefaList msg="Welcome to Your Vue.js Home" :tasks="listaDeTarefas" />
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

<style></style>
