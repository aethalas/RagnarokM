<template>
      <div>
    <b-container fluid>
      <b-row>
        <b-col lg="5" class="my-1">
          <b-form-group label="Filter" label-cols-sm="1" label-align-sm="right" label-size="sm" label-for="filterInput" class="mb-1">
            <b-input-group size="sm">
              <b-form-input v-model="filter" type="search" id="filterInput" placeholder="Type to Search"></b-form-input>
                <b-input-group-append>
                  <b-button :disabled="!filter" @click="filter = ''">Clear</b-button>
                </b-input-group-append>
              </b-input-group>
            </b-form-group>
          </b-col>
      </b-row>
    </b-container>


    <b-table id="my-table" :filter="filter" :per-page="perPage" :current-page="currentPage" striped hover head-variant="dark" table-variant="light" primary-key="id" :items="items" :fields="fields">
      <template v-slot:cell(icon)="data">
        <img :src="data.value" class="icon-image">
      </template>
      <template v-slot:cell(name)="data">
        <CardsModal :data="data"/>
      </template>
      <template v-slot:cell(mvp)="data">
        <p v-if="data.value == 'Normal'"><b-badge>{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Mini Boss'"><b-badge variant="info">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'MVP'"><b-badge variant="danger">{{data.value}}</b-badge></p>
      </template>
    </b-table>



    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
      align="right"
    ></b-pagination>

 </div>
</template>

<script>
  import axios from 'axios';
  import CardsModal from './CardsModal.vue'

  export default {
    components: {
      CardsModal
    },

    data() {
      return {
        perPage: 10,
        currentPage: 1,
        filter: null,
        filterOn: [],
        fields: [
          { key: 'icon', sortabe: false },
          { key: 'name', sortable: true },
          { key: 'slot', sortable: true },
          { key: 'mvp', sortable: true }
        ],
        items: [],
        errors: [],
        infoModal: {
          id: 'info-modal',
          title: '',
          content: ''
        }
      }
    },

    created() {
      axios.get('http://jonnyhtyson.com/ragnarokm/api/items.php?get=cards')
      .then(response => {
        this.items = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
    },

    computed: {
      rows ()
      {
        return this.items.length
      }
    }
  }
</script>

<style>

</style>