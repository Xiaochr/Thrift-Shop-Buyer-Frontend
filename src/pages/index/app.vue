<template>
  <div id="app">
    <img src="../../assets/logo.png">
    <login></login>
  </div>
</template>

<script>
import login from '../../components/login.vue'
export default {
  components: {
    login
  },
}
</script>

<style lang="postcss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
body {
  background: #F5F5F5;
}
</style>
