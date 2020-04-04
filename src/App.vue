<template>
  <div id="app">
    <div class="container">
      <header>
        <h1>Corona Virus <br> Real time updates</h1>
      </header>

      <body>
        <section class="computed-container">
            <span><h2>Total new confirmed:</h2>{{ totalNewConfirmed }}</span>
            <span><h2>Total confirmed:</h2>{{ totalConfirmed }}</span>
            <span><h2>Total recovered:</h2>{{ totalRecovered }}</span>
            <span><h2>Total deaths:</h2>{{ totalDeaths }}</span>
        </section>

      <div class=select>
        <country-list :countries="countries"/>
        <country-info :country="selectedCountry"></country-info>
      </div>
        
      </body>
    </div>
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
    this.get()
     eventBus.$on("country-selected", (country) => {this.selectedCountry = country});
  }
  
}
</script>

<style>
body {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(41, 41, 41);
  margin-top: 60px;
  font-size: 3vw;
}

.container {
  display: grid;
  max-width: 900px;
  position: relative;
  margin: auto;
  grid-gap: 5px;
  grid-template-columns: repeat(8, 100px);
  grid-template-rows: repeat(8, 100px); 
}

header {
  grid-area: 1 / 1 / span 3 / span 9;
   background-image: url("./assets/download.jpeg");
  /* background-repeat: no-repeat;
  background-position: center; */
   font-size: 1.5em;
  color: #ffffff;
  text-align: right;
 
}

h1 {
  margin-right: 3vw;
}

.computed-container {
  grid-area: 3 / 1 / span 2 / span 9;
  width: 100%;
  display: flex;
  flex-direction: row;
}

span {
  margin: 2rem 2rem;
  padding: 1rem 1rem;
  border: 0.5vw solid #db1e1e;
  background: #ffffff;
 
}

.select {
  grid-area: 5 / 3 / span 1 / span 2;
}


</style>
