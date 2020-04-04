<template>
  <div id="app">
   <h1>Corona Virus figures</h1>
   
   <div>Total new confirmed: {{ totalNewConfirmed }}</div>
   <div>Total confirmed: {{ totalConfirmed }}</div>
   <div>Total recovered: {{ totalRecovered }}</div>
   <div>Total deaths: {{ totalDeaths }}</div>

  <country-list :countries="countries"/>
  <country-info :country="selectedCountry"></country-info>

  </div>
</template>

<script>
import CountryList from './components/CountryList.vue'
import CountryInfo from './components/CountryInfo.vue'
import CountryChart from './components/CountryChart.vue'
import { eventBus } from './main.js';


export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: null,
      // pinnedCountries: []
    }
  },
  components: {
    "country-list": CountryList,
    "country-info": CountryInfo,
    "countries-chart": CountryChart
  },
  methods: {
    get: function() {
    fetch('https://api.covid19api.com/summary')
    .then(res => res.json())
    .then(data => this.countries = data.Countries)
    .catch( error => { console.log(error); })
    },
    addToPinnedd: function() {
      this.pinnedCountries.push(this.selectedCountry)
    }
},
  computed: {
    totalNewConfirmed: function() {
      return this.countries.reduce((sum, country) => sum + country.NewConfirmed, 0);
        },
    totalConfirmed: function() {
      return this.countries.reduce((sum, country) => sum + country.TotalConfirmed, 0);
    },  
    totalRecovered: function() {
      return this.countries.reduce((sum, country) => sum + country.TotalRecovered, 0);
    },  
    totalDeaths: function() {
      return this.countries.reduce((sum, country) => sum + country.TotalDeaths, 0);
    }
},
  mounted() {
    this.get(),
     eventBus.$on("country-selected", (country) => {this.selectedCountry = country});
  }
  
}
</script>

<style>
#app {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
