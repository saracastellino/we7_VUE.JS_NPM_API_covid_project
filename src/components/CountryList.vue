<template>
<div>
  <ul>
     <li v-for="(country, index) in countries" 
        :country="country" :key="index">{{ country }}</li>
  </ul>
  
</div>
 
</template>

<script>
export default {
  name: 'country-list',
  props: ["countries"]
 
}
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
