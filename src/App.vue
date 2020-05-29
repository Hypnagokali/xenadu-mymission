<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <TodoList msg="xenadu MyMission"/>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: green;
  width: 600px;
  margin: 0 auto;
  margin-top: 60px;
}
</style>
