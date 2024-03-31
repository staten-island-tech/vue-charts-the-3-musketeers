<template>
  <div>
<h1>2010 NYC Math SAT Scores</h1>
<canvas ref="pieChart" width="500" height="500"></canvas>
  </div>
</template>

<script setup >

import { ref, onMounted } from 'vue';
import Chart from 'chart.js/auto';
//import { Pie, Chart } from 'vue-chartjs'
//import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
//ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)


const pieChart = ref(null); 
const NY = ref('');

async function getmath(){
  try{
  let res = await fetch('https://data.cityofnewyork.us/resource/zt9s-n5aj.json')
  let data = await res.json()
  data = data.filter(school => school.mathematics_mean !== undefined && school.mathematics_mean !== null);
  NY.value = data;
  process(data);
  console.log(data);
} catch (error) {
    console.error('error fetching data:', error);
  }}

  function process(data) {
  let scoreRanges = {
    "200-299": 0,
    "300-399": 0,
    "400-499": 0,
    "500-599": 0,
    "600-699": 0,
    "700+": 0,
  };

  data.forEach(school => {
    let mathScore = parseInt(school.mathematics_mean);

    for (let range in scoreRanges) {
      let [min, max] = range.split('-').map(Number);

      if (mathScore >= min && mathScore <= max) {
        scoreRanges[range]++;
        break;
      }
    }
  });

  console.log(scoreRanges); 
  createPieChart(scoreRanges);
}

function createPieChart(scoreRanges){
  let labels = Object.keys(scoreRanges);
  let dataPoints = Object.values(scoreRanges);
  
  let totalSchools = dataPoints.reduce((acc, curr) => acc + curr, 0);
  
  let chartElement = pieChart.value;
  if (!chartElement) {
    console.error('nope');
    return;
  }
  
  new Chart(chartElement.getContext('2d'), {
    type: 'pie',
    data: {
      labels: labels,
      datasets: [{
        label: "% of Schools",
        data: dataPoints,
        backgroundColor:[
        'rgb(147, 47, 109)',
        'rgb(48, 82, 82)',
        'rgb(152, 210, 235)',
        'rgb(242, 100, 48)',
        'rgb(148, 168, 154)',
        'rgb(189, 76, 77)',
        ],
      }]
    }, 
    options: {
      plugins:{
        title: {
          display: true,
          text: "Percentages"
        },
        tooltip: {
          callbacks: {
            label: function(context) {
              let percentage = ((context.parsed / totalSchools) * 100).toFixed(2);
              return `${context.label}: ${percentage}%`;
            }
          }
        }
      }
    }
  });
}



onMounted(() => {
  getmath();
  
});


</script>
<style lang="css" scoped>
/* //this shit is not working */
div {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; 
}

canvas {
  margin-top: 0.5px; 
  font-family: 'Manrope', sans-serif;
}

h1 {
  text-align: center; 
  margin-bottom: 10px; 
  font-family: 'Manrope', sans-serif;
}
</style>

