<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <MainLayout
      msg="Fuck you bitch"
    />
  </div>
</template>

<script>
import MainLayout from './views/MainLayout.vue'

export default {
  name: 'App',
  components: {
    MainLayout
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
