<template>
  <div id="app" class="max-width">
    <Header/>
  </div>
</template>

<script>
import Header from './components/Header.vue'

export default {
  name: 'app',
  components: {
    Header
  }
}
</script>

<style>
  @import url("https://fonts.googleapis.com/icon?family=Material+Icons");
  @import url("https://fonts.googleapis.com/css?family=Rubik");

  #app {
    font-family: 'Rubik', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  * {
    box-sizing: border-box;
  }

  body {
    background: #ffffff;
    background-image: url("./assets/background.png");
    margin: 0;
  }

  .max-width {
    max-width: 1400px;
    margin: 0 auto;
  }

   @media (min-width: 1000px) and (max-width: 1400px) {
    .max-width {
      max-width: 85vw;
      margin: 0 auto;
    }
   }

    @media (min-width: 1px) and (max-width: 999px) {
    .max-width {
      max-width: 500px;
      margin: 0 auto;
    }
   }
</style>
