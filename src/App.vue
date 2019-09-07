<template>
  <div id="app">
    <ragnarok-m/>
  </div>
</template>

<script>
import RagnarokM from './components/RagnarokM.vue'

export default {
  name: 'app',
  components: {
    RagnarokM
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
