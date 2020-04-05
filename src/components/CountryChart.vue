<template>
	<GChart
		type="PieChart"
    :data="chartData"  
		:options="chartOptions"		
	/>
</template>

<script>
// import CountryInfo from './components/CountryInfo.vue'
import { GChart } from 'vue-google-charts';
// import { eventBus } from '../main.js';

export default {
  name: "GChart",
  props: ["country"],    
  data() {
    return {
      chartData: [   
        this.countries.NewConfirmed.value(country),
        this.countries.TotalConfirmed.value(ccountry),
        this.countries.TotalRecovered.value(country),
        this.countries.TotalDeaths.value(country)
        // this.countries.values(country)
        ],
      chartOptions: {
          chart: {
          is3D: true,
          backgroundColor: "rgba(3, 3, 3, 0.904)"
            }
          }
      };
  },
	components: {
		GChart
  },
  // mounted(){
  //   eventBus.$on('country-selected', (country) => {this.country = country})
  // }
};

