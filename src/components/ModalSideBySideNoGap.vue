<template>
  <b-row>
    <b-col lg="7">            
      <b-container>
        <ModalSideBySide :description="description1" :value="value1"/>
      </b-container>
    </b-col>
    <b-col v-if="description2 != ''">               
      <b-container>
        <ModalSideBySide :description="description2" :value="value2"/>
      </b-container>
    </b-col>
  </b-row>
</template>

<script>
  import ModalSideBySide from './ModalSideBySide.vue'

  export default {
    components: {
      ModalSideBySide
    },

    props: {
      description1: String,
      value1: String,
      description2: String,
      value2: String
    }
  }
</script>

<style scoped>

</style>