<template>
  <div id="app">
    <div class="container">
      <header class="blurred-box">
        <h1>Corona Virus <br> Real time updates</h1>
      </header>

      
        <section>
          <span><h2>Total new cases confirmed:</h2>{{ totalNewConfirmed | formatNumber }}</span>
            <span><h2>Total cases confirmed:</h2>{{ totalConfirmed | formatNumber }}</span>
            <span><h2>Total cases recovered:</h2>{{ totalRecovered | formatNumber }}</span>
            <span><h2>Total deaths:</h2>{{ totalDeaths | formatNumber }}</span>
        </section>
            
      <div class=select>
        <country-list :countries="countries"/>
        <country-info :country="selectedCountry"></country-info>
      </div>
   
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
      }
    // addToPinnedd: function() {
    //   this.pinnedCountries.push(this.selectedCountry)
    // }
  },
  filter: {
    formatNumber: function (num) {
        return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
        // return num.toLocaleString();
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

.container {
  display: grid;
  max-width: 100%;
  position: relative;
  margin: auto;
  grid-gap: 5px;
  grid-template-columns: repeat(12, 100px);
  grid-template-rows: repeat(12, 100px); 
}

body {
  grid-area: 4 / 1 / span 12 / span 12;
  background-image: url("./assets/background.png");
  background-position: cover;
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(41, 41, 41);
  font-size: 1,8vw;
  z-index: -10;
}

header {
  grid-area: 1 / 1 / span 3 / span 13;
  background-image: url("./assets/download.jpeg");
  /* background-attachment: fixed; */
  background-size: cover;
  max-width: 100%;
  height: auto;
  color: #ffffff;
  text-align: right;
}

h1 {
  font-size: 7vw;
  margin-right: 3vw;
  padding-bottom: 2vw;
  margin-bottom: 2vw;
}

section{
  grid-area: 4 / 5 / span 7 / span 8;
  background:rgba(100,100,100, 0.6);
}

span {
grid-area: 4 / 1 / span 3 / span 10;
  height: 20vw;
  display: inline-table;
  /* position: absolute; */
  width: 20vw;
  margin: 2rem 2rem;
  padding: 1rem 1rem;
  border: 0.5vw solid #5e1010;
  background: #ffffff;
}

div.select {
  grid-area: 4 / 1 / span 2 / span 3;
   background:rgba(100,100,100, 0.6);
}
/* IF COUNTRY SELECTED grid-area: 4 / 1 / span 4 / span 3; */

</style>
