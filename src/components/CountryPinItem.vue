<template lang="html">
<div v-if="country">
    <h3>{{country.Country}}</h3>
    <p>New confirmed: {{country.NewConfirmed}}</p>
    <p>Total confirmed: {{country.TotalConfirmed}}</p>
    <p>New deaths: {{country.NewDeaths}}</p>
    <p>Total deaths: {{country.TotalDeaths}}</p>
    <p>New recovered: {{country.NewRecovered}}</p>
    <p>Total recovered: {{country.TotalRecovered}}</p>
    <button v-on:click="removePin">Remove pin</button>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
   name: 'pinned-countries',
    data(){
    return {
      "pinnedCountry": []
    }
  },
  props: ["country"],
  methods: {
    removePin: function() {
      eventBus.$emit("pin-removed", this.country);
    }
  },
   mounted(){
    eventBus.$on('pinned-country', (country) => {this.country = country})
  }
};
</script>