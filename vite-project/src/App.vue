<template>
  <div>

<h1>Chart of NYC Writing SAT Scores in 2010</h1>
<canvas ref="pieChart" width="400" height="400"></canvas>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import { Pie } from 'vue-chartjs';


console.log("rachel says meow");


const NY = ref('')
async function getNY(){
  let res = await fetch('https://data.cityofnewyork.us/resource/zt9s-n5aj.json')
  let data = await res.json()
  NY.value = data
  console.log(data);
}
onMounted(()=>{
  getNY().then(() => {
    generatePieChart();
  });
});


  const scoreRanges = {
    '300-350': 0,
    '351-400': 0,
    '401-450': 0,
    '451-500': 0,
    '501-550': 0,
    '551-600': 0,
    '601-650': 0
  };





</script>

<style lang="scss" scoped>

</style>