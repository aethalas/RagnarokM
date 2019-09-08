<template>
  <div>
    <b-img :src="require('../assets/header.png')" fluid-grow></b-img>
    <b-card no-body>
      <b-tabs  pills card fill>
        <b-tab title="Monsters" active><Monsters/></b-tab>
        <b-tab title="Items"><Monsters/></b-tab>
        <b-tab title="Cards"><Monsters/></b-tab>
        <b-tab title="Equipment"><Monsters/></b-tab>
      </b-tabs>
    </b-card>
  </div>
</template>

<script>
  import Monsters from './Monsters.vue'

  export default {
    components: {
      Monsters
    }
  }
</script>

<style>

</style>