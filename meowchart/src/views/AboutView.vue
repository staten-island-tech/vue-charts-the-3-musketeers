<template>
    <div>

    </div>
</template>

<script setup>
import {ref, onMounted} from "vue"
const math = ref('')
async function getMaths(){
    let result = await fetch("https://data.cityofnewyork.us/resource/zt9s-n5aj.json?")
    let data = await result.json(
        math.value=data.results
    )
}
onBeforeMount(() => {
  getMaths();
});
</script>

<style scoped>

</style>