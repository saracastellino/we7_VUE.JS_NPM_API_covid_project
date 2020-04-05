<template>
  <div id="app">
    <div class="container">
      <header>
        <h1>Corona Virus <br> Real time updates</h1>
      </header>

       <section>
          <span><h2>Total new cases:</h2> <br> <h2 class="red">{{ totalNewConfirmed | formatNumber }}</h2></span>
          <span><h2>Total cases:</h2> <br> <h2 class="red">{{ totalConfirmed | formatNumber }}</h2></span>
          <span><h2>Total cases recovered:</h2> <br> <h2 class="red">{{ totalRecovered | formatNumber }}</h2></span>
          <span><h2>Total deaths:</h2> <br> <h2 class="red">{{ totalDeaths | formatNumber }}</h2></span>
      </section>
            
      <div class="select">
        <country-list :countries="countries"/>
        <country-info :country="country" :class="{selected: country = selectedCountry}"/>
        <GChart id="pie-chart" :country="country"/>
        <!-- <pinned-countries :country="pinnedCountries"></pinned-countries> -->
      </div>
       
       <img class="infographic" src="./assets/COVID-19-infographic.png" fluid-grow alt="COVID-19 infographic">
       <img class="community" src="./assets/community.jpeg" alt="Community action">

    </div>
  </div>
</template>

<script>
import CountryList from './components/CountryList.vue'
import CountryInfo from './components/CountryInfo.vue'
import CountryChart from './components/CountryChart.vue'
// import CountryPin from './components/CountryPin.vue'
import { eventBus } from './main.js';


export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: {},
      country: null
      // pinnedCountries: []
    }
  },
  components: {
    "country-list": CountryList,
    "country-info": CountryInfo,
    "GChart": CountryChart
    // "pinned-countries": CountryPin
  },
  methods: {
    get: function() {
      fetch('https://api.covid19api.com/summary')
      .then(res => res.json())
      .then(data => this.countries = data.Countries)
      .catch( error => { console.log(error); })
      },
    // addToPinnedd: function() {
    //   this.pinnedCountries.push(this.selectedCountry)
    // }
  },
  filters: {
    formatNumber: function (value) {
        return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
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
    grid-template-columns: repeat(10, 100px);
    grid-template-rows: repeat(10, 100px); 
    background-image: url("./assets/background.jpeg");
    background-position: cover;
    background-repeat:round;
    font-family: 'Lato', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: rgb(65, 65, 65);
    font-size: 1,8vw;
  }

  header {
    grid-area: 1 / 1 / span 3 / span 12;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-image: url("./assets/download.jpeg");
    background-size: cover;
    max-width: 100%;
    height: auto;
    color: #ffffff;
    text-align: right;
  }

  h1 {
    font-size: 5em;
    margin-right: 3vw;
    padding-bottom: 2vw;
    margin-bottom: 2vw;
    text-shadow: 0.5vw 0.5vw #494949;
  }

  .red {
    font-size: 3vw;
    color: #ffffff;
    margin: 2rem 2rem;
    padding: 1rem 1rem;
    background: #5e1010;
  }

  section{
    grid-area: 4 / 4 / span 7 / span 8;
    background:rgba(100,100,100, 0.6);
    margin-bottom: 0.46vw;
  }

  span {
    height: 280px;
    width: 280px;
    display: inline-table;
    margin: 1.5rem 1.5rem;
    padding: 0.5rem 0.5rem;
    border: 0.3vw solid #5e1010;
    background: #ffffff;
  }

  div.select {
    grid-area: 4 / 1 / span 2 / span 3;
    background:rgba(100,100,100, 0.6);
    padding-top: 1.5vw;
    padding-bottom: 6vw;
    color: #ffffff;
    z-index: 1;
    margin-left: 0.3em;
  }

  div.selected {
    grid-area: 4 / 1;
    background:rgba(3, 3, 3, 0.904);
    padding-bottom: 15.35em;
    padding-top: 0.5vw;
  }

  #pie-chart {
    height: 5em;
    width: max;
  }

  .infographic {
    grid-area: 8 / 1;
    width: 19em;
    margin-left: 0.3em;
  }

  .community {
    grid-area: 6 / 1 / span 2 / span 3;
    height: 10em;
    margin-top: 20px;
    margin-left: 0.3em;
  }

</style>
