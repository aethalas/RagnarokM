<template>
<div>
  <div v-for="item of items" v-bind:key="item">
    {{itemName}}
  </div>
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
        items: []
      }
    },


    created() {
      axios.get('http://jonnyhtyson.com/ragnarokm/api/items.php', { params: {popover: this.itemName }})
      .then(response => {
        this.items = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
    },

    props: {
      itemName: Object,
    },

    methods: {
      info(item, index, button) {
        this.monsModal.title = `Row index: ${index}`
        this.monsModal.icon = item.icon
        this.$root.$emit('bv::show::modal', this.monsModal.id, button)
      },

      resetInfoModal() {
        this.monsModal.title = ''
        this.monsModal.icon = ''
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
  .item-name-popover {
    font-family: 'Ubuntu', sans-serif;
    text-shadow: 2px 2px 4px #e6e6e6;
    font-weight: bold;
    vertical-align: middle; 
    border: none;
    border-radius: 15px;
    background: rgba(255, 255, 255,0);
    font-size: 0.8vw;
    color:#3aa1f7; 
    margin: 0;
  }

  .item-name-popover:hover {
    background:#3aa1f7;
    color:white;
    text-shadow: 2px 2px 4px #000000;
  }
</style>