<template>
	<GChart
		type="PieChart"
    :data="this.country"  
		:options="chartOptions"		
	/>
</template>

<script>
import CountryInfo from './components/CountryInfo.vue'
import { GChart } from 'vue-google-charts';
import { eventBus } from '../main.js';

export default {
  name: "GChart",
  props: ["country"],    
  data() {
    return {
      chartOptions: {
          chart: {
          is3D: true,
          backgroundColor: '#eeeeee'
            }
          }
      };
  },
	components: {
		GChart
  }
};