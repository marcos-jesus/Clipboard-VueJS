<template>
  <div id="app">
    <Clipboard name="Clipboard" height="300" width="500" />
  </div>
</template>

<script>
import Clipboard from './components/Clipboard.vue'
export default {
  name: 'App',
  components: {
    Clipboard
  },
  
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
