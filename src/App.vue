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
  background-image: url('../src/assets/KakaoTalk_Photo_2023-02-05-19-22-20.png');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: 100% 100%;
}
</style>
