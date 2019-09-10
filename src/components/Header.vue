<template>
  <div>
    <b-img :src="require('../assets/header.png')" fluid-grow></b-img>
    <b-card no-body>
      <b-tabs  pills card fill>
        <b-tab title="Home"></b-tab>
        <b-tab title="Monsters"><Monsters/></b-tab>
        <b-tab title="Items" active><Items/></b-tab>
        <b-tab title="Cards"><Items/></b-tab>
        <b-tab title="Equipment"><Items/></b-tab>
      </b-tabs>
    </b-card>
  </div>
</template>

<script>
  import Monsters from './Monsters.vue'
  import Items from './Items.vue'

  export default {
    components: {
      Monsters,
      Items
    }
  }
</script>

<style>

</style>