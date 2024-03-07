<template>
    <div>
        <h1>api url: https://data.cityofnewyork.us/resource/zt9s-n5aj.json?</h1>
    </div>
</template>

<script>
import {pie} from 'vue-chartjs'
const data = {
  labels: [
    '280-380',
    '381-550',
    '551-736'
  ],
  datasets: [{
    label: 'Number of Students',
    data: [300, 50, 100],
    backgroundColor: [
      'rgb(255, 99, 132)',
      'rgb(54, 162, 235)',
      'rgb(255, 205, 86)'
    ],
    hoverOffset: 4
  }]
};
</script>

<style scoped>

</style>