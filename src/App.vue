<template>
  <div id="app">
    <h2>Simple Todolist</h2>
    <br />
    <MainTodo />
  </div>
</template>

<script>
import MainTodo from "./components/MainTodo/MainTodo.vue";

export default {
  name: "App",
  components: {
    MainTodo
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
