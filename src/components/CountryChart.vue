<template>
	<g-chart
		type="PieChart"
        :data="chartData"
		:options="chartOptions"		
	></g-chart>
</template>

<script>
import { GChart } from 'vue-google-charts';

export default {
    name: "country-chart",
    props: ["selectedCountry"],    
    data() {
     return {
        chartData: [
          this.NewConfirmed,
          this.TotalConfirmed,
          this.TotalRecovered,
          this.TotalDeaths,
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
	}
};