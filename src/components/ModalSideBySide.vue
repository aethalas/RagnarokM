<template>
  <b-row>
    <b-col>
      <b>{{description}}</b>
    </b-col>
    <b-col>
      {{value}}
    </b-col>
  </b-row>
</template>

<script>
  export default {
    props: {
      description: String,
      value: String
    }
  }
</script>

<style scoped>

</style>