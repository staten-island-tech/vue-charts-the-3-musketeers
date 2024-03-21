<template>
  <div>
<h1>bleep bop</h1>
<canvas id="myChart"></canvas>
  </div>
</template>

<script setup>
console.log("rachel says meow");

import { Bar } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
import { ref, onMounted } from 'vue';

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)



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

const ctx = document.getElementById('myChart');

new 




</script>

<style lang="scss" scoped>

</style>
