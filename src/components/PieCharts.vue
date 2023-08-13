<script setup>
import { ref,defineProps, onMounted, onBeforeMount, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue'

defineProps({
    title:String
})

const newItem = ref(16)

let chart = null
const dataset = [300,50,100,200]
 // dataset can populed from fetch api or any other source
// but we need to beforeOnMounted hook for that

const data = {
  labels: [
    'Red',
    'Blue',
    'Yellow'
  ],
  datasets: [{
    label: 'My First Dataset',
    data: dataset,
    backgroundColor: [
      'rgb(255, 99, 132)',
      'rgb(54, 162, 235)',
      'rgb(255, 205, 86)'
    ],
    hoverOffset: 4
  }]
};

const config = {
  type: 'pie',
  data: data,
};

onMounted(()=>{
    const ctx = document.getElementById('myChart');
    chart = new Chart(ctx, config)
})

function updateChart(){
    // alert('Its working')
 dataset.push(newItem.value)
 chart.data.datasets[0].data = dataset
 chart.update()
}

onBeforeUnmount(() => {
  console.log('before Unmount')
//   satus.value.push('before Unmount')
})

</script>

<template>

<div >

<h3 class="text-2xl mb-10"> {{ title }}</h3>
<div class="mx-auto w-[500px] h-[600px] bg-slate-500">
   
  <canvas id="myChart"></canvas>
</div>

<div class="mt-20">
    <input type="text" v-model="newItem">
    <button @click="updateChart()" type="button" class="ml-2 bg-blue-600 hover:bg-blue-900 text-white py-2 px-4 rounded-md">Add</button>
</div>


</div>

</template>

<style scoped>

</style>