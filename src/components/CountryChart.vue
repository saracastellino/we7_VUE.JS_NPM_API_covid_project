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
    name: "countries-chart",
    props: ["country"],    
    data() {
        return {
              chartData: [
          this.totalNewConfirmed,
          this.totalConfirmed,
          this.totalRecovered,
          this.totalDeaths
          ],
        chartOptions: {
            chart: {
            title: "Covid-19 graph",
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