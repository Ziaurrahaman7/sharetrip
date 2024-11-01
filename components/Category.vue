<template>
    <nav class="space-x-6 hidden md:flex">
      <!-- Loop through the categories and render each as a link -->
      <nuxt-link
        v-for="(category, index) in categories"
        :key="index"
        class="text-gray-700 hover:text-indigo-500 cursor-pointer capitalize"
      >
        {{ category.name }}
      </nuxt-link>
    </nav>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const categories = ref([])
  
  const { data, pending, error } = await useFetch('https://dummyjson.com/products/categories')
  
  if (data.value) {
  categories.value = data.value.slice(0, 5)
}

if (error.value) {
  console.error("Error fetching categories:", error.value)
}
  </script>
  