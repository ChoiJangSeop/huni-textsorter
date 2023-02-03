<template>
  <MainPage />
</template>

<script>
import MainPage from './components/MainPage.vue';
export default {
  name: 'App',
  components: { MainPage },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  /* color: #2c3e50; */
  margin-top: 0px;
}
body {
  margin: 0;
  height: 100vh;
  background-color: #000000;
}
</style>
