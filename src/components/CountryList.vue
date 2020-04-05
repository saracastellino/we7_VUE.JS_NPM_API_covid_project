<template>
<div class="select">
   <label for="country-selected">View Country updates:</label>
      <select v-on:change.prevent="handleSelect" id="country-selected" v-model="selectedCountry">
        <option disabled value="">Select a country</option>
        <option v-for="(country, index) in countries" :country="country" :key="index">{{country.Country}}</option>
      </select>
</div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'country-list',
  data(){
    return {
      "selectedCountry": [],
    }
  },
  props: ["countries"],
  methods: {
    handleSelect(){
      eventBus.$emit('country-selected', this.selectedCountry)
    }
  }
}
</script>


<style scoped>

</style>
