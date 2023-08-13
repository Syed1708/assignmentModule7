<script setup>

import { defineProps, ref, onMounted, nextTick, onBeforeUnmount } from 'vue'
defineProps({
    title:String
})


const items = ref([
    'https://images.unsplash.com/photo-1691168223030-5e5cadfe07d1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1032&q=80',
    'https://images.unsplash.com/photo-1691520673295-9626f624869b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
    'https://images.unsplash.com/photo-1577624060070-ca1afe89ddad?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1026&q=80',
    'https://images.unsplash.com/photo-1605972643561-8bac9eec3ddc?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1032&q=80',
])

let carousel = null
const newItem = ref('https://images.unsplash.com/photo-1583794018021-c841442da0e3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80')

function addNewItem(){
    items.value.push(newItem.value)
    carousel.destroy()
    nextTick(()=>{
        carousel = new Flickity('#carousel')
    })
    
}

onMounted(()=>{
    carousel = new Flickity('#carousel',{
        cellAlign: 'left',
        contain: true
    })
})

onBeforeUnmount(() => {
  console.log('before Unmount')
//   satus.value.push('before Unmount')
})
</script>

<template>

<div >
    <div class="mt-20 mb-10">
        <h3 class="text-2xl mb-10">{{ title }}</h3>
    <input type="text" v-model="newItem">
    <button @click="addNewItem()" type="button" class="ml-2 bg-blue-600 hover:bg-blue-900 text-white py-2 px-4 rounded-md">Add New Image</button>
</div>

<div class="mx-auto items bg-slate-500" id="carousel">
    
 <div :style="`background-image:url(${item})`" class="item" v-for="(item,index) in items" :key="index">
    {{ index + 1 }}
</div>

</div>




</div>

</template>

<style scoped>
.items{
    width: 800px;
    height: 500px;
}
.item{
    width: 800px;
    height: 500px;
    background-color: bisque;
    background-size: cover;
}
</style>