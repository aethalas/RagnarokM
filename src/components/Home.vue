<template>
 <b-container fluid>
   <b-row>
     <b-col fluid="sm">Using Views! Much wow. So amaze.</b-col>
     <b-col fluid="sm">Need to do some more wizardry later.</b-col>
   </b-row> 

   <b-row>
     <b-col fluid="sm"><HomeRace/></b-col>
     <b-col fluid="sm"><HomeRace/></b-col>
     <b-col fluid="sm"><HomeRace/></b-col>
   </b-row>
 </b-container>
</template>

<script>
import HomeRace from './HomeRace.vue'

export default {
 components: {
  HomeRace
 }
}
</script>

<style>

</style>