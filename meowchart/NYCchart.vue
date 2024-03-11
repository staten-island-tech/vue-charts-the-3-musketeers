<template>
    <div>
        <h1>api url: </h1>
    </div>
</template>

<script setup>
import {pie} from 'vue-chartjs';
import { onBeforeMount } from 'vue';
const mathscores = ref("");
async function getMath(){
  let res = await fetch("https://data.cityofnewyork.us/resource/zt9s-n5aj.json?");
  let data = await res.json();
  mathscores.value = data.results;
}

onBeforeMount(() => {
  getMath();
});
const meow = {
  labels: [
    '280-380',
    '381-550',
    '551-736'
  ],
  datasets: [{
    label: 'Number of Students',
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