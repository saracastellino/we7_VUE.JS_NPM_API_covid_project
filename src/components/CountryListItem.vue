<template>
  <div>
    <li @click="show">{{ country.Country }}</li>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: "country-list-item",
  props: ["country"],
  methods: {
      show(){
          eventBus.$emit("country-selected", this.country);
      }
   }
}
</script>

<style scoped>

</style>