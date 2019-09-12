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
          <b-col>
            <b-form-group
              label="Type"
              label-cols-sm="6"
              label-cols-md="4"
              label-cols-lg="5"
              label-align-sm="right"
              label-size="sm"
              label-for="raceSelection"
              class="mb-1"
            >
              <b-form-select
                v-model="filter"
                id="raceSelection"
                size="sm"
                :options="type"
              ></b-form-select>
            </b-form-group>
          </b-col>
      </b-row>
    </b-container>


    <b-table id="my-table" :filter="filter" :per-page="perPage" :current-page="currentPage" striped hover head-variant="dark" table-variant="light" primary-key="id" :items="items" :fields="fields">
      <template v-slot:cell(icon)="data">
        <img :src="data.value" class="icon-image">
      </template>
      <template v-slot:cell(name)="data">
        <ItemsModal :data="data"/>
      </template>
      <template v-slot:cell(sellable)="data">
        <p v-if="data.value == 'Yes'"><b-badge variant="success">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'No'"><b-badge variant="danger">{{data.value}}</b-badge></p>
      </template>
      <template v-slot:cell(tradeable)="data">
        <p v-if="data.value == 'Yes'"><b-badge variant="success">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'No'"><b-badge variant="danger">{{data.value}}</b-badge></p>
      </template>
      <template v-slot:cell(storageable)="data">
        <p v-if="data.value == 'Yes'"><b-badge variant="success">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'No'"><b-badge variant="danger">{{data.value}}</b-badge></p>
      </template>
      <template v-slot:cell(type)="data">
        <p v-if="data.value == 'Common'"><b-badge variant="primary">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Potion'"><b-badge variant="secondary">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Refine'"><b-badge variant="success">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Scroll'"><b-badge variant="danger">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Blueprint'"><b-badge variant="warning">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Material'"><b-badge variant="info">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Equipment'"><b-badge variant="light">{{data.value}}</b-badge></p>
        <p v-if="data.value == 'Card'"><b-badge variant="dark">{{data.value}}</b-badge></p>
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
  import ItemsModal from './ItemsModal.vue'

  export default {
    components: {
      ItemsModal
    },

    data() {
      return {
        perPage: 10,
        currentPage: 1,
        filter: null,
        filterOn: [],
        type: ['Common', 'Potion', 'Refine', 'Scroll', 'Blueprint', 'Material', 'Equipment', 'Card'],
        fields: [
          { key: 'icon', sortabe: false },
          { key: 'name', sortable: true },
          { key: 'sellable', sortable: true },
          { key: 'tradeable', sortable: true },
          { key: 'storageable', sortable: true },
          { key: 'type', sortable: true }
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
      axios.get('http://jonnyhtyson.com/ragnarokm/api/items.php?get=equipment')
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