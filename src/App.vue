<script setup>

import { ref, onMounted, onBeforeMount, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue'

import PieCharts from './components/PieCharts.vue'
import Carousel from './components/Carousel.vue'



</script>

<template>
<div class="mx-auto container">

<PieCharts title="My PieChart"/>
<Carousel title="My Carousel"/>



</div>


</template>

<style scoped>

</style>
