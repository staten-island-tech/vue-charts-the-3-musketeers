<template>
  <div>

<h1>Chart of NYC Writing SAT Scores in 2010</h1>
<canvas ref="pieChart" width="400" height="400"></canvas>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import { Pie } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)


console.log("rachel says meow");

const NY = ref('');
async function getNY(){
  let res = await fetch('https://data.cityofnewyork.us/resource/zt9s-n5aj.json')
  let data = await res.json()
  data = data.filter(school => school.writing_mean !== undefined && school.writing_mean !== null);
  NY.value = data;
  process(data);
  console.log(data);
}

function process(data) {
  let scoreRanges = {
    "300-350": 0, 
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
    if (writingScore >= 300 && writingScore <= 350) {
      scoreRanges['300-350']++;
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

  console.log(scoreRanges); //amt of schools in score range

  let totalSchools = data.length;
  let percentages = {};
  for (let range in scoreRanges) {
    percentages[range] = Math.round((scoreRanges[range] / totalSchools) * 100);
  }

  console.log(percentages); //% of schools

  let chartData = {
    labels: [],
    datasets: [{
      data: [],
      backgroundColor: [
        '#FF6384',
        '#36A2EB',
        '#FFCE56',
        '#4BC0C0',
        '#9966FF',
        '#FF9900',
        '#0099CC'
      ]
    }]
  };

  for (let range in scoreRanges) {
    chartData.labels.push(range);
    chartData.datasets[0].data.push(scoreRanges[range]);
  }

  console.log(chartData);
}

onMounted(() => {
  getNY();
});












/* const NY = ref('')
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

function generatePieChart() {
  const scores = NY.value.map(school => parseInt(school.writing_score));


  const scoreRanges = {
    '300-350': 0,
    '351-400': 0,
    '401-450': 0,
    '451-500': 0,
    '501-550': 0,
    '551-600': 0,
    '601-650': 0
  };

  scores.forEach(score => {
    if (score >= 300 && score <= 350) {
      scoreRanges['300-350']++;
    } else if (score >= 351 && score <= 400) {
      scoreRanges['351-400']++;
    } else if (score >= 401 && score <= 450) {
      scoreRanges['401-450']++;
    } else if (score >= 451 && score <= 500) {
      scoreRanges['451-500']++;
    } else if (score >= 501 && score <= 550) {
      scoreRanges['501-550']++;
    } else if (score >= 551 && score <= 600) {
      scoreRanges['551-600']++;
    } else if (score >= 601 && score <= 650) {
      scoreRanges['601-650']++;
    }
  });
}
 */


</script>

<style lang="scss" scoped>

</style>