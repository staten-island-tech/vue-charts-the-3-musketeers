

<script setup>
import { ref, onBeforeMount } from 'vue'
const schools = ref('')
const schoolNames = ref('')
const mathScores = ref('')
const chartData = ref()
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

/* export default {
  name: 'BarChart',
  components: { Bar },
  data() {
    return {
      chartData: {
        labels: [ 'January', 'February', 'March'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979'  ,
            data: [40, 20, 12]
          }
        ]
      }
    }
  }
} */
/* export default {
  name: 'BarChart',
  components: { Bar },
  data: () => ({
    loaded: false,
    chartData: null
  }),
  async mounted () {
    this.loaded = false

    try {
      const { userlist } = await fetch('/api/userlist')
      this.chartdata = userlist

      this.loaded = true`
    } catch (e) {
      console.error(e)
    }
  }
} */
/* defineProps({
  chartData: {
        labels: [ 'January', 'February', 'March'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979'  ,
            data: [40, 20, 12]
          }
        ]
      }
}) */
let apidata = ref()
 const getsat = async()=>{
 let response = await fetch("https://data.cityofnewyork.us/resource/zt9s-n5aj.json");
     let data = await response.json();
     schoolNames.value = data.map(school =>{ 
      return school.school_name ? school.school_name : ""});
     mathScores.value = data.map(school =>{ 
      return school.critical_reading_mean ? parseInt(school.critical_reading_mean) : 0});
     schools.value = data;
     apidata = data
     /* chartData.value = {
      labels: schoolNames,
      datasets: [
        {
          label: 'Math!',
          data: mathScores,
          backgroundColor: '#f87979'
        }
      ]
    } */
    chartData.value = {
        labels: [ 'January', 'February', 'March'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979'  ,
            data: [40, 20, 12]
          }
        ]
      }
     console.log(chartData.value);
 }
 onBeforeMount(()=>{
   getsat();
   /* chartData.value = {
        labels: [ 'January', 'February', 'March'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979'  ,
            data: [40, 20, 12]
          }
        ]  
      } */
 })
</script>
<template>

<!-- <ol>
  <li v-for="x in schools">{{ x.number_of_test_takers }}</li>
</ol> -->
<div class="card" v-for="data in apidata">
  <h1>{{ data.school_name }}</h1>
</div>
<div>
<router-link to="/about">math</router-link>
<router-link to="/">home</router-link>
<router-link to="/english">english</router-link>
</div>
<div>
<router-view></router-view>
</div>
<!-- <div class="container">
    <Bar  :data="{
      labels: schoolNames,
      datasets: [
        {
          label: 'Reading!',
          data: mathScores,
          backgroundColor: '#f87979',
          maintainAspectRatio: false,
        },
      ],
      options: {
responsive: true,
maintainAspectRatio: false,
      },
    }" />
  </div> -->

  </template>
<style scoped>
/* v-if="loaded" */
.container {
  height: 1053px;
  width: 2109px;
}
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
