<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Txtinput/>
  </div>
</template>

<script>
import Txtinput from './components/Txtinput.vue'

export default {
  name: 'App',
  components: {
    Txtinput
  }
}
</script>

<style>
html,body {
  width: 100%;
  height: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
