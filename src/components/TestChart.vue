<template>
    <GChart
    type="PieChart"
    :data="chartData"
    :options="chartOptions"
  />
</template>

<script>
// import CountryInfo from './components/CountryInfo.vue'
// import { GChart } from 'vue-google-charts';
// import { eventBus } from '../main.js';

export default {
//   name: "GChart",
  props: ["country"],    
  data () {
    return {
      // Array will be automatically processed with visualization.arrayToDataTable function
      chartData: [
        // ["NewConfirmed", "TotalConfirmed", "TotalRecovered", "TotalDeaths"],
        // [this.country.NewConfirmed],
        // [this.country.TotalConfirmed],
        // [this.country.TotalRecovered],
        // [this.country.TotalDeaths]
      ],
      chartOptions: {
        chart: {
          is3D: true,
          backgroundColor: "rgba(3, 3, 3, 0.904)"
            }
      },
    //   components: {
	// 	"GChart": GChart
    //   },
    }
  }
}
</script>

<style>

</style>