<template>
  <div>
<h1>Chart of NYC Writing SAT Scores in 2010</h1>
<canvas ref="doughnutChart" width="300" height="300"></canvas>
  </div>
</template>

<script setup >

import { ref, onMounted } from 'vue';
import Chart from 'chart.js/auto';
//import { Doughnut } from 'vue-chartjs'
//import { Chart } from 'vue-chartjs';
//import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
//ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)


console.log("rachel says meow");

const doughnutChart = ref(null); // define doughnutchart ref thank jesus oh my gdo
const NY = ref('');

async function getNY(){
  try{
  let res = await fetch('https://data.cityofnewyork.us/resource/zt9s-n5aj.json')
  let data = await res.json()
  data = data.filter(school => school.writing_mean !== undefined && school.writing_mean !== null);
  NY.value = data;
  process(data);
  console.log(data);
} catch (error) {
    console.error('error fetching data:', error);
  }}

function process(data) {
  let scoreRanges = {
    "250-300": 0,
    "301-350": 0, 
    "351-400": 0, 
    "401-450": 0,
    "451-500": 0,
    "501-550": 0, 
    "551-600": 0,
    "601-650": 0,
    "651-700": 0,
  };

  data.forEach(school => {
    let writingScore = parseInt(school.writing_mean); 
    if (writingScore >= 250 && writingScore <= 300) {
      scoreRanges['250-300']++;
    } else if (writingScore <= 350) {
      scoreRanges['301-350']++;
    } else if (writingScore <= 400) {
      scoreRanges['351-400']++;
    } else if (writingScore <= 450) {
      scoreRanges['401-450']++;
    } else if (writingScore <= 500) {
      scoreRanges['451-500']++;
    } else if (writingScore <= 550) {
      scoreRanges['501-550']++;
    } else if (writingScore <= 600) {
      scoreRanges['551-600']++;
    } else if (writingScore <= 650) {
      scoreRanges['601-650']++;
    } else if (writingScore <= 700) {
      scoreRanges['651-700']++;
    } 
  });

  //console.log(scoreRanges); //amt of schools in score range

/*   let totalSchools = data.length;
  let percentages = {};
  for (let range in scoreRanges) {
    percentages[range] = Math.round((scoreRanges[range] / totalSchools) * 100);
  }

  console.log(percentages); //% of schools */

/*   let labels = [];
let dataPoints = [];

for(let range in scoreRanges){
  labels.push(range);
  dataPoints.push(scoreRanges[range]);
  
} */

createDoughnutChart(scoreRanges);
}

function createDoughnutChart(scoreRanges){
  let labels = Object.keys(scoreRanges);
  let dataPoints = Object.values(scoreRanges);
  
  let chartElement = doughnutChart.value;
  if (!chartElement) {
    console.error('THIS SHIT NOT WORKING');
    return;
  }
  
  
  
  new Chart(chartElement.getContext('2d'), {
    type: 'doughnut',
    data: {
      labels: labels,
      datasets: [{
        label: "Schools",
        data: dataPoints,
        backgroundColor:[
          '#41B883', '#E46651', '#00D8FF', '#DD1B16', '#99F949', '#E45681', '#01D3FF', '#DF1C86', '#FF9C86',
        ],
      }]
    }, 
    options: {
      plugins:{
        title: {
          display: true,
          text: "NYC HS SAT Writing Scores 2010"
        }
      }
    }

  });
}


onMounted(() => {
  getNY();
  
});


</script>

<style lang="scss" scoped>

</style>
