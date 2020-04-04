<template lang="html">
  <div v-if="country">
    <h3>{{country.Country}}</h3>
    <p>New confirmed: {{country.NewConfirmed}}</p>
    <p>Total confirmed: {{country.TotalConfirmed}}</p>
    <p>New deaths: {{country.NewDeaths}}</p>
    <p>Total deaths: {{country.TotalDeaths}}</p>
    <p>New recovered: {{country.NewRecovered}}</p>
    <p>Total recovered: {{country.TotalRecovered}}</p>
    <!-- CHART -->
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'country-info',
  props: ["country"]
}
</script>

<style scoped>

</style>