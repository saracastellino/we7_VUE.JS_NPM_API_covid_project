<template>
	<g-chart
		type="PieChart"
    :data="chartData"
		:options="chartOptions"		
	></g-chart>
</template>

<script>
import { GChart } from 'vue-google-charts';
import { eventBus } from '../main.js';

export default {
  name: "country-chart",
  props: ["country"],    
  data() {
    return {
      chartData: [
          this.country        
        // this.country.NewConfirmed,
        // this.country.TotalConfirmed,
        // this.country.TotalRecovered,
        // this.country.TotalDeaths
        ],
      chartOptions: {
          chart: {
          title: `Covid-19 in {{ this }}`,
          is3D: true,
          backgroundColor: '#eeeeee'
            }
          }
      };
  },
	components: {
		"g-chart": GChart
  },
  mounted(){
    eventBus.$on('country-selected', (country) => {this.country = country})
  }
};