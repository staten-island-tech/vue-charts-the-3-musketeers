<script setup>
import { ref, onBeforeMount, onMounted } from 'vue'
import {useRoute} from 'vue-router'
const schoolNames = ref('')
const schools = ref('')
const searchValue = ref('staten')
const route = useRoute()
  

const getsat = async()=>{
 let response = await fetch("https://data.cityofnewyork.us/resource/zt9s-n5aj.json");
     let data = await response.json();
     

     schoolNames.value = data.map(school =>{ 
      return school.school_name ? school.school_name : ""});
     schools.value = data;
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
 }
 onBeforeMount(()=>{
   /* getsat(); */
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
 
  getsat();

</script>

<template>
  <div>
    <p>All NYC high schools:</p>
    <ol>
      <li v-for="school in schools">{{ school.school_name }}</li>
    </ol>
  </div>
</template>
