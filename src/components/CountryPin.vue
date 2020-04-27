<template>
<div>
    
      <label v-if='country'><h2>Pinned countries:</h2></label>
      <select v-on:change.prevent="handleSelect" id="pinned-country" v-model="country">
        <option disabled value="">Select a country</option>
        <option v-for="(country, index) in pinnedCountries" :country="country" :key="index">{{country}}</option>
      </select>
  
</div>
</template>

<script>
import CountryInfo from './CountryInfo.vue';
import { eventBus } from '../main.js';

export default {
    name: 'pinned-countries',
    data(){
    return {
      'country': null,
      "pinnedCountries": [],
      'pinnedCountry': null
    }
  },
    // props: ['pinnedCountry'],
     components: {
    "country-info": CountryInfo
     },
  // methods: {
  //   },
  //    handleSelect(){
  //     let pinnedCountry;
  //     this.countries.forEach(country => {
  //       if(country.Country == this.pinnedCountry)
  //       pinnedCountry = country;
  //     });
  //     eventBus.$emit('country-pinned', pinnedCountry)
  //    }
  //  },
 mounted(){
        eventBus.$on('pinned-country', (country) => {alert({country})}); 
      //  {this.country = country}
     
 }
}
</script>

<style scoped>

</style>