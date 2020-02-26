<template>
  <div>
    <b-img :src="require('../assets/header.png')" fluid-grow></b-img>
    <b-card no-body>
      <b-tabs  pills card fill>
        <b-tab title="Home" active><Home/></b-tab>
        <b-tab title="Jobs" disabled></b-tab>
        <b-tab title="Monsters"><Monsters/></b-tab>
        <b-tab title="Items"><Items/></b-tab>
        <b-tab title="Cards"><Cards/></b-tab>
        <b-tab title="Equipment"><Equipment/></b-tab>
      </b-tabs>
    </b-card>
  </div>
</template>

<script>
  import Home from './Home.vue'
  import Monsters from './Monsters.vue'
  import Items from './Items.vue'
  import Cards from './Cards.vue'
  import Equipment from './Equipment.vue'

  export default {
    components: {
      Home,
      Monsters,
      Items,
      Cards,
      Equipment
    }
  }
</script>

<style>

</style>