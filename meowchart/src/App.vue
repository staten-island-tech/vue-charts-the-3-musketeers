<template>
  <div>
      <h1>Math Scores Organized by % (6 ranges)</h1>

  </div>
</template>

<script setup>
import {ref, onBeforeMount} from "vue"
import { Pie } from "vue-chartjs"
import { Chart as ChartJS, Title, Tooltip, Legend, PieController, CategoryScale, LinearScale } from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, PieController, CategoryScale, LinearScale)


// sort schools by score ranges (6 total ranges)
//then just put that data into the pie chart. add the number of schools that are in each range
const math = ref('')
async function getMaths(){
  let res = await fetch('https://data.cityofnewyork.us/resource/zt9s-n5aj.json?')
  let data = await res.json();
  math.value=data.results
}
onBeforeMount(() => {
getMaths();
});

// use a for each/loop to iterate through the list, then for each # that is within
//the range, just add from --> [0], or the previous #.
// USE IF/ELSE?????

for (let i = 0; i < data.length; i++){
  
}

const meow = {
labels: [
  '200-299',
  '300-399',
  '400-499',
  '500-599',
  '600-699',
  '700+',
],
datasets: [{
  label: '% of Schools',
  backgroundColor: [
    'rgb(147, 47, 109)',
    'rgb(48, 82, 82)',
    'rgb(152, 210, 235)',
    'rgb(242, 100, 48)',
    'rgb(148, 168, 154)',
    'rgb(189, 76, 77)',
  ],
  hoverOffset: 4
}]
}; 
</script>

<style scoped>

</style>