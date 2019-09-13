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
              label="Rank"
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
                :options="rank"
          ></b-form-select>
          </b-form-group>
        </b-col>
      </b-row>
    </b-container>

    <b-table id="my-table" :filter="filter" :per-page="perPage" :current-page="currentPage" striped hover head-variant="dark" table-variant="light" primary-key="id" :items="monsters" :fields="fields">
      <template v-slot:cell(icon)="data">
        <img :src="data.value" class="icon-image">
      </template>
      <template v-slot:cell(name)="data">
        <MonsterModal :data="data"/>
      </template>
      <template v-slot:cell(size)="data">
        {{data.value}}
      </template>
      <template v-slot:cell(rank)="data">
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
        rank: ['Normal', 'Mini Boss', 'MVP'],
        fields: [
          { key: 'icon', sortabe: false },
          { key: 'name', sortable: true },
          { key: 'level', sortable: true },
          { key: 'race', sortable: true },
          { key: 'element', sortable: true },
          { key: 'rank', sortable: true }
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
      axios.get('http://jonnyhtyson.com/ragnarokm/api/monster.php?get=all')
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
 img {
   width: 64px;
 }

 .table > tbody > tr > td {
    vertical-align: middle;
    font-family: 'Ubuntu', sans-serif;
    text-shadow: 2px 2px 4px #d5d5d5;
  }

  @media (min-width: 1000px) and (max-width: 1400px) {

  }

  @media (min-width: 1px) and (max-width: 999px) {
    img {
      width: 40px;
    }

    .table > tbody > tr > td {
      vertical-align: middle;
      font-family: 'Ubuntu', sans-serif;
      text-shadow: 2px 2px 4px #d5d5d5;
      padding: 0 !important;
      margin: 0 !important;
    }
  }
</style>