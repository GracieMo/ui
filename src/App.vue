<template>
    <Navi/>
</template>

<script>
import Navi from './components/reserve.vue'

export default {
  name: 'app',
  components: {
    Navi,
  }
}
</script>

<style>
  * {
    margin: 0px;
    padding: 0px;
  }
  html, body {
    height: 100%;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
