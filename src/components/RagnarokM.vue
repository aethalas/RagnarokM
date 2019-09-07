<template>
 <div>
  <b-table striped hover :items="monsters"></b-table>
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