<template lang="html">
  <div v-if="country">
    <h3>{{country.Country}}</h3>
    <p>New confirmed: {{country.NewConfirmed}}</p>
    <p>Total confirmed: {{country.TotalConfirmed}}</p>
    <p>New deaths: {{country.NewDeaths}}</p>
    <p>Total deaths: {{country.TotalDeaths}}</p>
    <p>New recovered: {{country.NewRecovered}}</p>
    <p>Total recovered: {{country.TotalRecovered}}</p>
    <!-- <countries-chart id="pie-chart" :countries="countries"></countries-chart> -->
  </div>
</template>

<script>
// import CountryChart from './components/CountryChart.vue'
import { eventBus } from '../main.js';

export default {
  name: 'country-info',
   data(){
    return {
      country: null
    }
  },
  mounted(){
    eventBus.$on('country-selected', (country) => {
      this.country = country
    })
  }
}
</script>

<style scoped>

</style>