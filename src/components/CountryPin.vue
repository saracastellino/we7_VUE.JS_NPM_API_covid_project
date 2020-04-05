<template>
<div class="" v-if="country">
    <h1>Pinned Countries</h1>
  <ul>
      <li v-for="(country, index) in country" :country="country" :key="index">{{country}}</li>
    </ul>
</div>
</template>

<script>
import CountryInfo from './components/CountryInfo.vue'

export default {
    name: 'pinned-countries',
    props: ['country'],
    components:{
        "country-info" :CountryInfo
    }
}
</script>

<style scoped>

</style>