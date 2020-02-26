<template>
 <b-table id="my-table" :filter="filter" :per-page="perPage" :current-page="currentPage" striped hover head-variant="dark" table-variant="light" primary-key="id" :items="monsters" :fields="fields">
 </b-table>
</template>

<script>
import axios from 'axios';

export default {
    data() {
      return {
        perPage: 10,
        currentPage: 1,
        filter: null,
        filterOn: [],
        race: ['Angel', 'Brute', 'Demi-Human', 'Demon', 'Dragon', 'Fish', 'Formless', 'Insect', 'Plant', 'Undead'],
        fields: [
          { key: 'Race', sortable: true },
          { key: 'Amount', sortable: true }
        ],
        monsters: [],
        errors: [],
      }
    },

    created() {
      axios.get('http://jonnyhtyson.com/ragnarokm/api/monster.php?get=stats')
      .then(response => {
        this.monsters = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
    },

    computed: {
      rows ()
      {
        return this.monsters.length
      }
    }
}
</script>

<style>

</style>