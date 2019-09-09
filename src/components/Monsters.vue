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
              label="Race"
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
                :options="race"
              ></b-form-select>
            </b-form-group>
          </b-col>
      </b-row>

      <b-row>
        <b-col lg="5" class="my-1">
          <b-form-group
              label="Element"
              label-cols-sm="6"
              label-cols-md="4"
              label-cols-lg="2"
              label-align-sm="right"
              label-size="sm"
              label-for="elementSelection"
              class="mb-1"
          >
          <b-form-select
                v-model="filter"
                id="elementSelection"
                size="sm"
                :options="element"
          ></b-form-select>
          </b-form-group>
        </b-col>

        <b-col>
          <b-form-group
              label="Size"
              label-cols-sm="6"
              label-cols-md="4"
              label-cols-lg="5"
              label-align-sm="right"
              label-size="sm"
              label-for="sizeSelection"
              class="mb-1"
          >
          <b-form-select
                v-model="filter"
                id="sizeSelection"
                size="sm"
                :options="size"
          ></b-form-select>
          </b-form-group>
        </b-col>
      </b-row>
    </b-container>


    <b-table id="my-table" :filter="filter" :per-page="perPage" :current-page="currentPage" striped hover head-variant="dark" table-variant="light" primary-key="id" :items="monsters" :fields="fields">
      <template v-slot:cell(icon)="data">
        <img :src="data.value">
      </template>
      <template v-slot:cell(name)="data">
        <b-button size="md" @click="info(data.item, data.index, $event.target)" class="mr-1">
          {{data.value}}
        </b-button>
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
  import MonsterModal from './MonsterModal.vue'

  export default {
    components: {
      MonsterModal
    },

    data() {
      return {
        perPage: 10,
        currentPage: 1,
        filter: null,
        filterOn: [],
        race: ['Angel', 'Brute', 'Demi-Human', 'Demon', 'Dragon', 'Fish', 'Formless', 'Insect', 'Plant', 'Undead'],
        element: ['Earth', 'Fire', 'Formless', 'Ghost', 'Holy', 'Neutral', 'Poison', 'Shadow', 'Undead', 'Water', 'Wind'],
        size: ['Small', 'Medium', 'Large'],
        fields: [
          { key: 'icon', sortabe: false },
          { key: 'name', sortable: true},
          { key: 'level', sortable: true},
          { key: 'race', sortable: true},
          { key: 'element', sortable: true},
          { key: 'size', sortable: true}
        ],
        monsters: [],
        errors: [],
        infoModal: {
          id: 'info-modal',
          title: '',
          content: ''
        }
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
    },

    computed: {
      rows ()
      {
        return this.monsters.length
      }
    },

    methods: {
      info(item, index, button) {
        this.infoModal.title = `Row index: ${index}`
        this.infoModal.content = JSON.stringify(item, null, 2)
        this.$root.$emit('bv::show::modal', this.infoModal.id, button)
      },
      resetInfoModal() {
        this.infoModal.title = ''
        this.infoModal.content = ''
      },
      onFiltered(filteredItems) {
        // Trigger pagination to update the number of buttons/pages due to filtering
        this.totalRows = filteredItems.length
        this.currentPage = 1
      }
    }
  }
</script>

<style>
 img {
   width: 64px;
 }
</style>