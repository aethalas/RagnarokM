<template>
  <div class="button-area">
    <b-modal v-if="isOpen" id="modal-xl" size="xl" hide-footer hide-header-close no-close-on-esc no-close-on-backdrop content-class="shadow" header-bg-variant="dark">
      <template v-slot:modal-title>
        <b-container class="monster-header">
          <b-row>
            <b-col cols="3" xs="auto" sm="auto" md="auto" lg="auto"><img :src="monsModal.icon" class="monster-icon-top"></b-col>
            <b-col cols="9" xs="auto" sm="auto" md="auto" lg="auto">
              <b>{{data.value}}</b><br>
              {{monsModal.race}} / {{monsModal.element}} / {{monsModal.size}}<br>
              <p v-if="monsModal.rank == 'Normal'"><b-badge>{{monsModal.rank}}</b-badge></p>
              <p v-if="monsModal.rank == 'Mini Boss'"><b-badge variant="info">{{monsModal.rank}}</b-badge></p>
              <p v-if="monsModal.rank == 'MVP'"><b-badge variant="danger">{{monsModal.rank}}</b-badge></p>
            </b-col>
          </b-row>
        </b-container>
      </template>

      <b-container>
        <b-row>
          <b-col class="monster-information">
            <b-container>

              <b-row>
                <b-col>
                  <b>Level</b>
                </b-col>
                <b-col>
                  {{monsModal.level}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Race</b>
                </b-col>
                <b-col>
                  {{monsModal.race}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Element</b>
                </b-col>
                <b-col>
                  {{monsModal.element}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Size</b>
                </b-col>
                <b-col>
                  {{monsModal.size}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Base Exp</b>
                </b-col>
                <b-col>
                  {{monsModal.baseExp}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Job Exp</b>
                </b-col>
                <b-col>
                  {{monsModal.jobExp}}
                </b-col>
              </b-row>

            </b-container>
          </b-col>

          <b-col class="monster-information">
            <b-container>

              <b-row>
                <b-col>
                  <b>Str</b>
                </b-col>
                <b-col>
                  {{monsModal.str}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Agi</b>
                </b-col>
                <b-col>
                  {{monsModal.agi}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Vit</b>
                </b-col>
                <b-col>
                  {{monsModal.vit}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Int</b>
                </b-col>
                <b-col>
                  {{monsModal.intellect}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Dex</b>
                </b-col>
                <b-col>
                  {{monsModal.dex}}
                </b-col>
              </b-row>

              <b-row>
                <b-col>
                  <b>Luk</b>
                </b-col>
                <b-col>
                  {{monsModal.luk}}
                </b-col>
              </b-row>

            </b-container>
          </b-col>

        </b-row>
      </b-container>

      <div v-if="monsModal.description" class="monster-description">{{monsModal.description}}</div>

      <b-container>
        <b-row>
          <b-col class="monster-statistics">
            <b-container>

              <b-row>
                <b-container>

                  <b-row>
                    <b-col>
                     
                      <b-container>
                        <b-row>
                          <b-col>
                            <b>HP</b>
                          </b-col>
                          <b-col>
                            {{monsModal.hp}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>Hit</b>
                          </b-col>
                          <b-col>
                            {{monsModal.hit}}
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
                            <b>Atk</b>
                          </b-col>
                          <b-col>
                            {{monsModal.atk}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>M.Atk</b>
                          </b-col>
                          <b-col>
                            {{monsModal.matk}}
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
                            <b>Def</b>
                          </b-col>
                          <b-col>
                            {{monsModal.def}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>M.Def</b>
                          </b-col>
                          <b-col>
                            {{monsModal.mdef}}
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
                            <b>Flee</b>
                          </b-col>
                          <b-col>
                            {{monsModal.flee}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
                     <b-container>
                        <b-row>
                          <b-col>
                            <b>Move Spd</b>
                          </b-col>
                          <b-col>
                            {{monsModal.movespeed}}
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
                            <b>Attack Spd</b>
                          </b-col>
                          <b-col>
                            {{monsModal.aspd}}
                          </b-col>
                        </b-row>
                      </b-container>

                    </b-col>
                    <b-col>
                      
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

      <div class="monster-statistics-loot">
        <b-container>
          <b-row>

            <b-col md="6" v-for="loot of lootTable" v-bind:key="loot" class="monster-loot-table">
              
              <b-container>
                <b-row>
                  <b-col cols="0.5">
                    <img :src="loot.icon" class="loot-icon">
                  </b-col>


                  <b-col cols="7">
                    <b>{{loot.itemName}}</b>
                  </b-col>

                  <b-col>
                    x {{loot.amount}}
                  </b-col>

                  
                  <b-col cols="0.5">
                    <b-badge v-if="loot.dropChance > 0" variant="success">{{loot.dropChance}}%</b-badge>
                  </b-col>
                </b-row>
              </b-container>
              
            </b-col>

          </b-row>
        </b-container>
      </div>

      <b-button class="item-name" block @click="isOpen = false;">Close</b-button>
    </b-modal>

    <b-button v-if="data.item.rank == 'Normal'" class="normal" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
    <b-button v-if="data.item.rank == 'Mini Boss'" class="mini-boss" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
    <b-button v-if="data.item.rank == 'MVP'" class="mvp" v-b-modal.modal-xl @click="isOpen = !isOpen; info(data.item, data.index, $event.target)">{{data.value}}</b-button>
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
        lootTable: [],
        errors: []
      }
    },

    created() {
      axios.get('http://jonnyhtyson.com/ragnarokm/api/monster.php', { params: {items: this.data.value }})
      .then(response => {
        // JSON responses are automatically parsed.
        this.lootTable = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
    },

    props: {
      data: Object
    },

    methods: {
      info(item, index, button) {
        this.monsModal.title = `Row index: ${index}`
        this.monsModal.icon = item.icon
        this.monsModal.rank = item.rank
        this.monsModal.race = item.race
        this.monsModal.element = item.element
        this.monsModal.size = item.size
        this.monsModal.description = item.description
        this.monsModal.level = item.level
        this.monsModal.baseExp = item.base_exp
        this.monsModal.jobExp = item.job_exp
        this.monsModal.str = item.str
        this.monsModal.agi = item.agi
        this.monsModal.vit = item.vit
        this.monsModal.intellect = item.intellect
        this.monsModal.dex = item.dex
        this.monsModal.luk = item.luk
        this.monsModal.hp = item.hp
        this.monsModal.atk = item.atk
        this.monsModal.def = item.def
        this.monsModal.hit = item.hit
        this.monsModal.aspd = item.aspd
        this.monsModal.flee = item.flee
        this.monsModal.matk = item.matk
        this.monsModal.mdef = item.mdef
        this.monsModal.movespeed = item.movespeed
        this.$root.$emit('bv::show::modal', this.monsModal.id, button)
      },

      resetInfoModal() {
        this.monsModal.title = ''
        this.monsModal.icon = ''
        this.monsMOdal.rank = ''
        this.monsModal.race = ''
        this.monsModal.element = ''
        this.monsModal.size =''
        this.monsModal.description = ''
        this.monsModal.level = ''
        this.monsModal.baseExp = ''
        this.monsModal.jobExp = ''
        this.monsModal.str = ''
        this.monsModal.agi = ''
        this.monsModal.vit = ''
        this.monsModal.intellect = ''
        this.monsModal.dex = ''
        this.monsModal.luk = ''
        this.monsModal.hp = ''
        this.monsModal.atk = ''
        this.monsModal.def = ''
        this.monsModal.hit = ''
        this.monsModal.aspd = ''
        this.monsModal.flee = ''
        this.monsModal.matk = ''
        this.monsModal.mdef = ''
        this.monsModal.movespeed = ''
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
  @import url("https://fonts.googleapis.com/css?family=Ubuntu");
  @import url("https://fonts.googleapis.com/css?family=Rubik");
  
  .monster-icon-top {
    height: 100px;
    width: 100px;
  }

  .button-area {
    padding-bottom: 10px;
  }

  .monster-header {
    font-family: 'Rubik', sans-serif;
    text-shadow: 2px 2px 4px #000000;
    color:#ffffff; 
    font-size: 22px;
  }

  .monster-description {
    font-family: 'Ubuntu', sans-serif;
    border-radius: 15px;
    background: #eff6ff;
    padding: 1vw; 
    width: 100%;
    font-size: 20px;
    text-shadow: 2px 2px 4px #d5d5d5;
  }

  .monster-information {
    font-family: 'Ubuntu', sans-serif;
    border-radius: 15px;
    background: #dfdfdf;
    padding: 1vw; 
    width: 100%;
    font-size: 20px;
    margin: 5px;
    text-shadow: 2px 2px 4px #d5d5d5;

    background: repeating-linear-gradient(
      120deg,
      #ffffff,
      #ffffff 10px,
      #f5f5f5 10px,
      #f5f5f5 20px
    );
  }

  .monster-statistics {
    font-family: 'Ubuntu', sans-serif;
    border-radius: 15px;
    background: #dfdfdf;
    padding: 1vw; 
    width: 100%;
    font-size: 20px;
    margin: 5px;
    text-shadow: 2px 2px 4px #d5d5d5;

    background: repeating-linear-gradient(
      120deg,
      #ffffff,
      #ffffff 10px,
      #f8f9ff 10px,
      #f8f9ff 20px
    );
  }

  .monster-statistics-loot {
    font-family: 'Ubuntu', sans-serif;
    border-radius: 15px;
    background: #dfdfdf;
    padding: 1vw; 
    width: 100%;
    font-size: 20px;
    margin: 5px;
    text-shadow: 2px 2px 4px #d5d5d5;

    background: repeating-linear-gradient(
      120deg,
      #ffffff,
      #ffffff 10px,
      #fffaf8 10px,
      #fffaf8 20px
    );
  }

  .monster-loot-table {
    margin-top: 2px;
    font-size: 16px;
  }

  .loot-icon {
    height: 20px;
    width: 20px;
  }

  .mvp {
    font-family: 'Ubuntu', sans-serif;
    text-shadow: 2px 2px 4px #e6e6e6;
    font-weight: bold;
    vertical-align: top; 
    width: 100%;
    height: 50px;
    border: none;
    border-radius: 15px;
    background: rgba(255, 255, 255,0);
    font-size: 0.8vw;
    color:#dc3545; 
    margin: 0;
  }

  .mvp:hover {
    background:#dc3545;
    color:white;
    text-shadow: 2px 2px 4px #000000;
  }

  .mini-boss {
    font-family: 'Ubuntu', sans-serif;
    text-shadow: 2px 2px 4px #e6e6e6;
    font-weight: bold;
    vertical-align: top; 
    width: 100%;
    height: 50px;
    border: none;
    border-radius: 15px;
    background: rgba(255, 255, 255,0);
    font-size: 0.8vw;
    color:#1aa2b8; 
    margin: 0;
  }

  .mini-boss:hover {
    background:#1aa2b8;
    color:white;
    text-shadow: 2px 2px 4px #000000;
  }
 
  .item-name {
    font-family: 'Ubuntu', sans-serif;
    text-shadow: 2px 2px 4px #e6e6e6;
    font-weight: bold;
    vertical-align: top; 
    width: 100%;
    height: 50px;
    border: none;
    border-radius: 15px;
    background: rgba(255, 255, 255,0);
    font-size: 0.8vw;
    color:#3aa1f7; 
    margin: 0;
  }

  .item-name:hover {
    background:#3aa1f7;
    color:white;
    text-shadow: 2px 2px 4px #000000;
  }

  .normal {
    font-family: 'Ubuntu', sans-serif;
    text-shadow: 2px 2px 4px #e6e6e6;
    font-weight: bold;
    vertical-align: top; 
    width: 100%;
    height: 50px;
    border: none;
    border-radius: 15px;
    background: rgba(255, 255, 255,0);
    font-size: 0.8vw;
    color:#6c757d; 
    margin: 0;
  }

  .normal:hover {
    background:#6c757d;
    color:white;
    text-shadow: 2px 2px 4px #000000;
  }

  @media (min-width: 1000px) and (max-width: 1400px) {
    .monster-icon-top {
      height: 95px;
      width: 95px;
    }

    .monster-information {
      font-size: 1.4vw;
    }

    .monster-description {
      font-size: 1.4vw;
    }

    .monster-statistics {
      font-size: 1.4vw;
    }

    .monster-statistics-loot {
      font-size: 1.4vw;
    }

    .monster-loot-table {
      font-size: 1.2vw;
    }

    .mt-3 {
      font-size: 1.5vw;
    }
  }

  @media (min-width: 1px) and (max-width: 999px) {
    .monster-icon-top {
      height: 60px;
      width: 60px;
    }

    .monster-information {
      font-size: 13px;
      margin: 1px;
    }

    .monster-header {
      font-size: 15px;
    }

    .monster-description {
      font-size: 13px;
    }

    .monster-statistics {
      font-size: 13px;
      margin: 1px;
    }

    .monster-statistics-loot {
      font-size: 13px;
      margin: 1px;
      padding: 5px; 
    }

    .monster-loot-table {
      font-size: 10px;
    }

    .loot-icon {
      height: 12px;
      width: 12px;
    }

    .normal {
      font-size: 12px;
    }

    .mini-boss {
      font-size: 12px;
    }

    .mvp {
      font-size: 12px;
    }
  }
</style>