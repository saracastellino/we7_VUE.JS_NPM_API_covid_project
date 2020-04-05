<template lang="html">
  <div v-if="country">
    <h3>{{country.Country}}</h3>
    <p>New confirmed: {{country.NewConfirmed}}</p>
    <p>Total confirmed: {{country.TotalConfirmed}}</p>
    <p>New deaths: {{country.NewDeaths}}</p>
    <p>Total deaths: {{country.TotalDeaths}}</p>
    <p>New recovered: {{country.NewRecovered}}</p>
    <p>Total recovered: {{country.TotalRecovered}}</p>
    <GChart id="pie-chart" :country="country"/>
    <!-- <button v-on:click="handleButton">Pin Country</button> -->
  </div>
</template>

<script>
import CountryChart from './CountryChart.vue'
import { eventBus } from '../main.js';

export default {
  name: 'country-info',
   data(){
    return {
      country: null
    }
  },
  components: {
    "GChart": CountryChart
  },
  // methods: {
  //   handleButton(){ 
  //    eventBus.$emit('pinned-country', this.country.Country)
  //   }
  // },
  mounted(){
    eventBus.$on('country-selected', (country) => {this.country = country})
  }
}
</script>

<style scoped>

</style>