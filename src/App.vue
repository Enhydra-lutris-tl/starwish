<template>
  <starBack/>
  <starCanvas/>

</template>

<script>
import starCanvas from './components/starCanvas.vue'
import starBack from './components/starBack'
export default {
  name: 'App',
  components: {
    starCanvas,
    starBack
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
