<template>
  <div class="button-area">
    <b-modal v-if="isOpen" id="modal-xl" size="xl" hide-footer hide-header-close no-close-on-esc no-close-on-backdrop content-class="shadow" header-bg-variant="dark">
      <template v-slot:modal-title>
        <b-container class="monster-header">
          <b-row>
            <b-col xs="auto" sm="auto" md="auto" lg="auto">
              <b>{{data.value}}</b>
            </b-col>
          </b-row>
        </b-container>
      </template>



     <b-container>
        <b-row>
          <b-col cols="3" align="center" class="monster-statistics">
            <b-container>

              <b-row>
                <b-col>
                  <img :src="monsModal.icon" class="monster-card-icon">
                </b-col>
              </b-row>

            </b-container>
          </b-col>

          <b-col class="monster-information">
            <b-container>

              <b-row>
                <b-col>
                  <b>Type</b>
                </b-col>
                <b-col>
                  <p v-if="monsModal.mvp == 'Normal'"><b-badge>{{monsModal.mvp}}</b-badge></p>
                  <p v-if="monsModal.mvp == 'Mini Boss'"><b-badge variant="info">{{monsModal.mvp}}</b-badge></p>
                  <p v-if="monsModal.mvp == 'MVP'"><b-badge variant="danger">{{monsModal.mvp}}</b-badge></p>
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Slot</b>
                </b-col>
                <b-col>
                  {{monsModal.slot}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Loot / Draw / Craft Card</b>
                </b-col>
                <b-col>
                  {{monsModal.loot_draw_craft}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Deposit Card</b>
                </b-col>
                <b-col>
                  {{monsModal.deposit}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Effects</b>
                </b-col>
                <b-col>
                  {{monsModal.effects}}
                </b-col>
              </b-row>

            </b-container>
          </b-col>

        </b-row>
      </b-container>

      <div class="monster-statistics-loot" v-if="droppedBy.length > 0">
        <b-container><b>Dropped By:</b>
          <b-row>

            <b-col md="6" v-for="drop of droppedBy" v-bind:key="drop" class="monster-loot-table">
              <b-container>
                <b-row>
                  <b-col cols="0.5">
                    <img :src="drop.icon" class="loot-icon">
                  </b-col>

                  <b-col cols="6">
                    <b>{{drop.monster_name}}</b>
                  </b-col>

                  <b-col cols="1">
                    <b-badge v-if="drop.drop_chance > 0" variant="success">{{drop.drop_chance}}%</b-badge>
                  </b-col>
                </b-row>
              </b-container>
            </b-col>
          </b-row>
        </b-container>
      </div>

      <b-button class="item-name" block @click="isOpen = false;">Close</b-button>
    </b-modal>

    <b-button v-if="data.item.mvp == 'Normal'" class="normal" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
    <b-button v-if="data.item.mvp == 'Mini Boss'" class="mini-boss" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
    <b-button v-if="data.item.mvp == 'MVP'" class="mvp" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    data ()
    {
      return {
        isOpen: false,
        monsModal: {
        id: 'info-modal',
        title: '',
        description: ''
        },
        droppedBy: [],
        errors: []
      }
    },

    props: {
      data: Object
    },

    created() {
      axios.get('http://jonnyhtyson.com/ragnarokm/api/items.php', { params: {monsters: this.data.value }})
      .then(response => {
        // JSON responses are automatically parsed.
        this.droppedBy = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
    },

    methods: {
      info(item, index, button) {
        this.monsModal.title = `Row index: ${index}`
        this.monsModal.icon = item.icon
        this.monsModal.mvp = item.mvp
        this.monsModal.slot = item.slot
        this.monsModal.effects = item.effects
        this.monsModal.loot_draw_craft = item.loot_draw_craft
        this.monsModal.deposit = item.deposit
        this.$root.$emit('bv::show::modal', this.monsModal.id, button)
      },

      resetInfoModal() {
        this.monsModal.title = ''
        this.monsModal.icon = ''
        this.monsModal.type = ''
        this.monsModal.slot = ''
        this.monsModal.effects = ''
        this.monsModal.loot_draw_craft = ''
        this.monsModal.deposit = ''
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
 .monster-card-icon {
   width: 200px;
 }
 
  @media (min-width: 1px) and (max-width: 999px) {
    .monster-card-icon {
      width: 60px;
    }
  }
</style>