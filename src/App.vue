<template>
  <div id="app">
   <h1>Corona Virus figures</h1>
   <country-list :countries="countries"/>
   <div>Total deaths: {{ totalDeaths }}</div>
  
  </div>
</template>

<script>
import CountryList from './components/CountryList.vue'

export default {
  name: 'App',
  data() {
    return {
      countries: []
    }
  },
  components: {
    "country-list": CountryList
  },
  methods: {
    get: function() {
    fetch('https://api.covid19api.com/summary')
    .then(res => res.json())
    .then(countries => this.countries = countries)
    .catch( error => { console.log(error); })
    },
    
},
  computed: {
    totalDeaths: function() {
      return this.countries.reduce((sum, country) => sum + country.TotalDeaths, 0);
        }    
},
  mounted() {
    this.get()
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
