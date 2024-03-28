<script setup>
import {ref} from 'vue'
import {useRouter} from 'vue-router'
const searchValue = ref('staten')
const router = useRouter()
const search = ()=>{
  router.push({
    name:"english",
    query: {value: searchValue.value}
  })
  
  
}

</script>

<template>
  <div class="card" v-if="data" v-for="data in data">
  <h1>{{ data.school_name }}</h1>
</div>
<div style="height: 400px; width: 400px">
<label for="searchfield">
  search for school:
</label>
<input id="searchfield" v-model="searchValue"/>
<button @click="search">search</button>
</div> 
</template>
