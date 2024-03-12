<template>
  <div>
<h1>bleep bop</h1>
  </div>
</template>

<script setup>
console.log("rachel says meow");

import { ref, onMounted } from 'vue';
const NY = ref('')
async function getNY(){
  let res = await fetch('https://data.cityofnewyork.us/resource/zt9s-n5aj.json')
  let data = await res.json()
  NY.value = data
  console.log(data);
}
onMounted(()=>{
  getNY()
});





</script>

<style lang="scss" scoped>

</style>
