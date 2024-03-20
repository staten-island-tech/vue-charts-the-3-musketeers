<template>
    <div>
        <canvas id="mychart"></canvas>

    </div>
</template>

<script setup>
import {ref, onBeforeMount} from "vue"
import { Pie } from "vue-chartjs"
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

/* const math = ref('')
async function getMaths(){
    let res = await fetch('https://data.cityofnewyork.us/resource/zt9s-n5aj.json?')
    let data = await res.json(
        math.value=data.results
    )
}
onBeforeMount(() => {
  getMaths();
}); */
</script>

<style scoped>

</style>