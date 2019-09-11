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
          <b-col cols="2" align="center" class="monster-statistics">
            <b-container>

              <b-row>
                <b-col>
                  <img :src="monsModal.icon" class="item-icon">
                </b-col>
              </b-row>

            </b-container>
          </b-col>

          <b-col class="monster-information">

            <b-container>

              <b-row>
                <b-container>

                  <b-row>
                    <b-col>
                     
                      <b-container>
                        <b-row>
                          <b-col>
                            <b>Type</b>
                          </b-col>
                          <b-col>
                            {{monsModal.type}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>Level</b>
                          </b-col>
                          <b-col>
                            {{monsModal.level}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                  </b-row>

                  <b-row>
                    <b-col>
                     
                      <b-container>
                        <b-row>
                          <b-col>
                            <b>Max Stack</b>
                          </b-col>
                          <b-col>
                            {{monsModal.max_stack}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>Sellable</b>
                          </b-col>
                          <b-col>
                            {{monsModal.sellable}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                  </b-row>

                  <b-row>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>Tradeable</b>
                          </b-col>
                          <b-col>
                            {{monsModal.tradeable}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>

                    <b-col>
                     
                      <b-container>
                        <b-row>
                          <b-col>
                            <b>Storageable</b>
                          </b-col>
                          <b-col>
                            {{monsModal.storageable}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>

                  </b-row>

                  <b-row>
                    
                    <b-col v-if="monsModal.sell_price > 0">
                     
                      <b-container>
                        <b-row>
                          <b-col>
                            <b>Sell Price</b>
                          </b-col>
                          <b-col>
                            {{monsModal.sell_price}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
              
                    <b-col v-if="monsModal.sell_price > 0">
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            
                          </b-col>
                          <b-col>
                            
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                  </b-row>

                </b-container>
              </b-row>

            </b-container>

          </b-col>

        </b-row>
      </b-container>

      <div v-if="monsModal.description" class="monster-description">{{monsModal.description}}</div>

      <div v-if="monsModal.equip_type">
      <b-container>
        <b-row>
          <b-col class="monster-information">
            <b-container>

              <b-row>
                <b-container>

                  <b-row>
                    <b-col>
                     
                      <b-container>
                        <b-row>
                          <b-col>
                            <b>Equipment Type</b>
                          </b-col>
                          <b-col>
                            {{monsModal.equip_type}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>Jobs</b>
                          </b-col>
                          <b-col>
                            {{monsModal.jobs}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                  </b-row>


                </b-container>
              </b-row>

            </b-container>
          </b-col>

        </b-row>
      </b-container>
      </div>

      <div v-if="monsModal.effects" class="monster-statistics"><b>Item Effects</b><br>{{monsModal.effects}}</div>

      <div v-if="monsModal.upgrade_of" class="monster-information">Upgrade Of: <b>{{monsModal.upgrade_of}}</b></div>

      <b-button class="item-name" block @click="isOpen = false;">Close</b-button>
    </b-modal>

    <b-button class="item-name" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
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
      }
    },

    props: {
      data: Object
    },

    methods: {
      info(item, index, button) {
        this.monsModal.title = `Row index: ${index}`
        this.monsModal.icon = item.icon
        this.monsModal.description = item.description
        this.monsModal.type = item.type
        this.monsModal.level = item.level
        this.monsModal.max_stack = item.max_stack
        this.monsModal.sellable = item.sellable
        this.monsModal.sell_price = item.sell_price
        this.monsModal.tradeable = item.tradeable
        this.monsModal.storageable = item.storageable
        this.monsModal.equip_type = item.equip_type
        this.monsModal.jobs = item.jobs
        this.monsModal.effects = item.effects
        this.monsModal.upgrade_of = item.upgrade_of
        this.$root.$emit('bv::show::modal', this.monsModal.id, button)
      },

      resetInfoModal() {
        this.monsModal.title = ''
        this.monsModal.icon = ''
        this.monsModal.description = ''
        this.monsModal.type = ''
        this.monsModal.level = ''
        this.monsModal.max_stack = ''
        this.monsModal.sellable = ''
        this.monsModal.sell_price = ''
        this.monsModal.tradeable = ''
        this.monsModal.storageable = ''
        this.monsModal.equip_type = ''
        this.monsModal.jobs = ''
        this.monsModal.effects = ''
        this.monsModal.upgrade_of = ''
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
 .item-icon {
   width: 100px;
   height: 100px;
 }
</style>