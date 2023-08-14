<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
//array of images
const images =[
'https://images.unsplash.com/photo-1610413260327-ac5ffe5e0146?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
'https://images.unsplash.com/photo-1612712191426-54db4d88cbec?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
'https://images.unsplash.com/photo-1490772888775-55fceea286b8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
'https://images.unsplash.com/photo-1502082553048-f009c37129b9?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
'https://images.unsplash.com/photo-1490730141103-6cac27aaab94?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
'https://images.unsplash.com/photo-1490750967868-88aa4486c946?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80'
  
];

const currentIndex = ref(0)

const nextSlide =() =>{
  clearInterval(autoSlideInterval)
  currentIndex.value = (currentIndex.value + 1) % images.length
  startAutoSlide()

}

const prevSlide =() =>{
  clearInterval(autoSlideInterval)
  currentIndex.value = (currentIndex.value - 1 + images.length) % images.length
  startAutoSlide()
}

let autoSlideInterval;

onMounted(() => {
  startAutoSlide()
})

onBeforeUnmount(() => {
  clearInterval(autoSlideInterval)
})

function startAutoSlide() {
  autoSlideInterval = setInterval(()=>{
    nextSlide()
  }, 3000)
}

</script>

<template>
  <div class="text-center mt-10"> <h1 class="text-4xl font-bold text-rose-500">A Carousel with Vue.js </h1></div>
  <div class="flex justify-center items-center"> 
    <div class="w-2/3 h-2/3 relative mt-10">
      <img :src="images[currentIndex]" alt="Carousel slide" class="h-96 w-full mx-4 rounded-md shadow-md relative">
      <button @click="prevSlide" class="absolute left-10 top-1/2 transform -translate-y-1/2 px-4 py-2 bg-gray-300 text-gray-800 rounded-full text-2xl">
        &lt;
      </button>
      <button @click="nextSlide" class="absolute right-10 top-1/2 transform -translate-y-1/2 px-4 py-2 bg-gray-300 text-gray-800 rounded-full text-2xl">
        &gt;
      </button>
    </div>
  </div>
</template>


<style scoped>

.slide {
  transition: transform 0.5s ease-in-out;
}

</style>
