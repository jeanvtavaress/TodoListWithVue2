<template>
  <div id="app">
     <TheTodoList />




  </div>
</template>

<script>
import TheTodoList from './components/TheTodoList.vue'

export default {
  name: 'App',
  components: {
    TheTodoList
  }
}
</script>

<style>
body {
  background-color: rgb(101, 145, 212);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  margin-top: 60px;
}
</style>
