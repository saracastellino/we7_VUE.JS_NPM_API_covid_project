<template>
<div class="select">
   <label for="country-selected"><h2>View Country updates:</h2></label>
      <select v-on:change.prevent="handleSelect" id="country-selected" v-model="selectedCountry">
        <option disabled value="">Select a country</option>
        <option v-for="(country, index) in countries" :country="country" :key="index">{{country.Country}}</option>
      </select>
</div>
</template>

<script>
import { eventBus } from '../main.js'
import CountryPinVue from './CountryPin.vue';

export default {
  name: 'country-list',
  data(){
    return {
      "selectedCountry": {}
    }
  },
  //  components: {
  //   "pinned-country": CountryPin
  //    },
  props: ["countries"],
  methods: {
    handleSelect(){
      let selectedCountry;
      this.countries.forEach(country => {
        if(country.Country == this.selectedCountry)
        selectedCountry = country;
      });
      
      eventBus.$emit('country-selected', selectedCountry)

    }
  }
}
</script>


<style scoped>

</style>
