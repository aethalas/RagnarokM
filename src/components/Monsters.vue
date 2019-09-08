<template>
 <div>
  <b-table striped hover head-variant="dark" table-variant="light" primary-key="id" :items="monsters" :fields="fields">
    <template v-slot:cell(icon)="data">
      <img :src="data.value">
    </template>
    <template v-slot:cell(name)="data">
      <b>{{data.value}}</b><br>
      <b>{{data.level}}</b>
    </template>
  </b-table>
 </div>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        fields: ['icon', 'name', 'level', 'hp'],
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
 img {
   width: 64px;
 }
</style>