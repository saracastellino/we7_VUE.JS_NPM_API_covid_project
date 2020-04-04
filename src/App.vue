<template>
  <div id="app">
   <h1>Corona Virus figures</h1>
   <!-- <country-list :countries="countries"/> -->
   <div>Total new confirmed: {{ totalNewConfirmed }}</div>
   <div>Total confirmed: {{ totalConfirmed }}</div>
   <div>Total recovered: {{ totalRecovered }}</div>
   <div>Total deaths: {{ totalDeaths }}</div>

<countries-chart id="pie-chart" :countries="countries"></countries-chart>

   <label for="country-selected">Select a Country:</label>
      <select id="country-selected" v-model="selectedCountry">
        <option disabled value="">Select a country</option>
        <option v-for="(country, index) in countries" :country="country" :key="index">{{country.Country}}</option>
      </select>

 <country-info
        v-if="selectedCountry"
        :country="selectedCountry"
      ></country-info>

  </div>
</template>

<script>
import CountryList from './components/CountryList.vue'
import CountryInfo from './components/CountryInfo.vue'
import CountryChart from './components/CountryChart.vue'


export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: null,
      pinnedCountries: []
    }
  },
  components: {
    "country-list": CountryList,
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
     eventBus.$on("country-selected", (country) => (this.selectedCountry = country));
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
