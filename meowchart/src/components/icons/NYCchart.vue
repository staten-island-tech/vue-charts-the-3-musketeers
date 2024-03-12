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