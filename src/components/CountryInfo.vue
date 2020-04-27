<template lang="html">
  <div v-if="country">
    <h3>{{country.Country}}</h3>
    <p>New confirmed: {{country.NewConfirmed}}</p>
    <p>Total confirmed: {{country.TotalConfirmed}}</p>
    <p>New deaths: {{country.NewDeaths}}</p>
    <p>Total deaths: {{country.TotalDeaths}}</p>
    <p>New recovered: {{country.NewRecovered}}</p>
    <p>Total recovered: {{country.TotalRecovered}}</p>
    <button @click="addToPinned" id="pinned-country" v-model="pinnedCountries">Pin Country</button>
    <TestChart :country="country"/>
    <!-- <CountryChart /> -->
  </div>
</template>

<script>
// import CountryChart from './CountryChart.vue'
import TestChart from './TestChart.vue'
import { eventBus } from '../main.js';

export default {
  name: 'country-info',
   data(){
    return {
      'country': null,
      'pinnedCountries': [],
      'pinnedCountry': null
    }
  },
  components: {
    // "CountryChart": CountryChart,
    "TestChart": TestChart
  },
  methods: {
    addToPinned(){
    //  this.country = this.pinnedCountry
     this.pinnedCountries.push(this.country)
     eventBus.$emit('pinned-country', this.country) 
      this.country = null;
    }
  },
  mounted(){
    eventBus.$on('country-selected', (country) => {this.country = country})
  }
}
</script>

<style scoped>

</style>