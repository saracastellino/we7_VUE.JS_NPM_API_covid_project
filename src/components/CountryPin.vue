<template>
<div>
    <h1>Pinned Countries</h1>
  
</div>
</template>

<script>
import CountryInfo from './CountryInfo.vue'

export default {
    name: 'pinned-countries',
    data(){
    return {
      "pinnedCountry": []
    }
  },
    props: ['country'],
    mounted(){
    eventBus.$on('pinned-country', (country) => {this.country = country})
  }
}
</script>

<style scoped>

</style>