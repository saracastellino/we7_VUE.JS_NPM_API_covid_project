<template>
<div>
   <label for="country-selected">Select a Country:</label>
      <select v-on:click="handleSelect" id="country-selected" v-model="selectedCountry">
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
      "selectedCountry": {},
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
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
