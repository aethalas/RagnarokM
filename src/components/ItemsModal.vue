<template>
    <div class="button-area">
    <b-modal v-if="isOpen" id="modal-xl" size="xl" hide-footer hide-header-close no-close-on-esc no-close-on-backdrop content-class="shadow" header-bg-variant="dark">
      <template v-slot:modal-title>
        <b-container class="monster-header">
          <b-row>
            <b-col xs="auto" sm="auto" md="auto" lg="auto">
              <b>{{data.value}}</b><br>{{monsModal.type}}
            </b-col>
          </b-row>
        </b-container>
      </template>



     <b-container>
        <b-row align-v="center">
          <b-col md="2" align="center">
            <b-container>

              <b-row>
                <b-col>
                  <img :src="monsModal.icon">
                </b-col>
              </b-row>

            </b-container>
          </b-col>

          <b-col md="5" class="monster-information">

            <b-container>

              <b-row v-if="monsModal.equip_type">
                <b-col>
                  <b-container>
                    <b-row>
                      <b-col>
                        <b>Slot</b>
                      </b-col>
                      <b-col>
                        {{monsModal.equip_type}}
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
              </b-row>

              <b-row>
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

            </b-container>

          </b-col>

          <b-col class="monster-information">

            <b-container>
              <b-row>
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
              </b-row>

              <b-row>
                <b-col>
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
              </b-row>

              <b-row v-if="monsModal.jobs">
                <b-col>
                  <b-container>
                    <b-row>
                      <b-col>
                        <b>Jobs</b>
                      </b-col>
                      <b-col :inner-html.prop="monsModal.jobs | jobsCheck">
                         
                      </b-col>
                    </b-row>
                  </b-container>
                </b-col>
              </b-row>

            </b-container>

          </b-col>

        </b-row>
      </b-container>

      <div v-if="monsModal.upgrade_of || monsModal.upgradeable_to" class="monster-information">
        <b-container>
          <b-row>
            <b-col v-if="monsModal.upgrade_of">
              Upgrade Of: <b>{{monsModal.upgrade_of}}</b>
            </b-col>
            <b-col v-if="monsModal.upgradeable_to" align="right">
              Upgrade To: <b>{{monsModal.upgradeable_to}}</b>
            </b-col>
          </b-row>
        </b-container>
        
      </div>

      <div v-if="monsModal.description" align="center" class="monster-description">{{monsModal.description}}</div>

      <div v-if="monsModal.effects" class="monster-statistics" :inner-html.prop="monsModal.effects"></div>

      
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

    <b-button class="item-name" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {

    data ()
    {
      return {
        test: 5,
        isOpen: false,
        monsModal: {
        id: 'info-modal',
        title: '',
        description: '',
        },
        droppedBy: [],
        errors: []
      }
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

    filters: {
      jobsCheck: function(string) {
        var classCheck = '';
        if (string.includes("thief"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Thief.png' class='job-icon'>  ";
        }
        if (string.includes("assassin"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Assassin.png' class='job-icon'> ";
        }
        if (string.includes("guillotine-cross"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Guillotine-Cross.png' class='job-icon'>  ";
        }
        if (string.includes("assassin-cross"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Assassin-Cross.png' class='job-icon'>  ";
        }
        if (string.includes("rogue"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Rogue.png' class='job-icon'> ";
        }
        if (string.includes("stalker"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Stalker.png' class='job-icon'>  ";
        }
        if (string.includes("shadow-chaser"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Shadow-Chaser.png' class='job-icon'>  ";
        }

        if (string.includes("merchant"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Merchant.png' class='job-icon'>  ";
        }
        if (string.includes("blacksmith"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Blacksmith.png' class='job-icon'>  ";
        }
        if (string.includes("whitesmith"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Whitesmith.png' class='job-icon'>  ";
        }
        if (string.includes("mechanic"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Mechanic.png' class='job-icon'>  ";
        }
        if (string.includes("alchemist"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Alchemist.png' class='job-icon'>  ";
        }
        if (string.includes("biochemist"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Biochemist.png' class='job-icon'>  ";
        }
        if (string.includes("geneticist"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Geneticist.png' class='job-icon'>  ";
        }

        if (string.includes("acolyte"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Acolyte.png' class='job-icon'>  ";
        }
        if (string.includes("priest"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Priest.png' class='job-icon'>  ";
        }
        if (string.includes("high-priest"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/High-Priest.png' class='job-icon'>  ";
        }
        if (string.includes("arc-bishop"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Arc-Bishop.png' class='job-icon'>  ";
        }
        if (string.includes("monk"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Monk.png' class='job-icon'>  ";
        }
        if (string.includes("champion"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Champion.png' class='job-icon'>  ";
        }
        if (string.includes("sura"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Sura.png' class='job-icon'>  ";
        }

        if (string.includes("archer"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Archer.png' class='job-icon'>  ";
        }
        if (string.includes("hunter"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Hunter.png' class='job-icon'>  ";
        }
        if (string.includes("sniper"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Sniper.png' class='job-icon'>  ";
        }
        if (string.includes("ranger"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Ranger.png' class='job-icon'>  ";
        }
        if (string.includes("bard"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Bard.png' class='job-icon'>  ";
        }
        if (string.includes("minstrel"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Minstrel.png' class='job-icon'>  ";
        }
        if (string.includes("maestro"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Maestro.png' class='job-icon'>  ";
        }
        if (string.includes("dancer"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Dancer.png' class='job-icon'>  ";
        }
        if (string.includes("gypsy"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Gypsy.png' class='job-icon'>  ";
        }
        if (string.includes("wanderer"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Wanderer.png' class='job-icon'>  ";
        }

        if (string.includes("magician"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Magician.png' class='job-icon'> ";
        }
        if (string.includes("wizard"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Wizard.png' class='job-icon'> ";
        }
        if (string.includes("high-wizard"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/High-Wizard.png' class='job-icon'> ";
        }
        if (string.includes("warlock"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Warlock.png' class='job-icon'> ";
        }
        if (string.includes("sage"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Sage.png' class='job-icon'> ";
        }
        if (string.includes("scholar"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Scholar.png' class='job-icon'> ";
        }
        if (string.includes("sorcerer"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Sorcerer.png' class='job-icon'> ";
        }

        if (string.includes("swordsman"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Swordsman.png' class='job-icon'> ";
        }
        if (string.includes("knight"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Knight.png' class='job-icon'> ";
        }
        if (string.includes("lord-knight"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Lord-Knight.png' class='job-icon'> ";
        }
        if (string.includes("rune-knight"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Rune-Knight.png' class='job-icon'> ";
        }
        if (string.includes("crusader"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Crusader.png' class='job-icon'> ";
        }
        if (string.includes("paladin"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Paladin.png' class='job-icon'> ";
        }
        if (string.includes("royal-guard"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Royal-Guard.png' class='job-icon'> ";
        }

        if (string.includes("novice"))
        {
          classCheck = classCheck + "<img src='http://jonnyhtyson.com/ragnarokm/images/classes/Novice.png' class='job-icon'>  ";
        }

        if (string.includes("any"))
        {
          classCheck = classCheck + "Any ";
        }

        return classCheck;
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
        this.monsModal.upgradeable_to = item.upgradeable_to
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
        this.monsModal.upgradeable_to = ''
      },

      onFiltered(filteredItems) {
        // Trigger pagination to update the number of buttons/pages due to filtering
        this.totalRows = filteredItems.length
        this.currentPage = 1
      },
    }
  }
</script>

<style>
  ul, li {
    margin: 0;
  }

 .item-icon {
   width: 100px;
   height: 100px;
 }

 .job-icon {
   width: 25px;
   height: 25px;
 }

 
</style>