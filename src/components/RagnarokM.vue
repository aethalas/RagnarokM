<template>
 <div>
   <div v-for="(entry, index) in monsters" :key="index">
     {{entry.name}}
   </div>
 </div>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        monsters: [],
        errors: []
      }
    },

    created() {
      axios.get('http://jonnyhtyson.com/ragnarokm/api/monster.php')
      .then(response => {
        this.monsters = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  }
</script>

<style>

</style>