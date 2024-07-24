<template>
  <div id="app">
    <MarvelSlider msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import MarvelSlider from './components/MarvelSlider.vue'

export default {
  name: 'App',
  components: {
    MarvelSlider
  }
}
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
