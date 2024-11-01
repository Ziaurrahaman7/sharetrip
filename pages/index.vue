<template>
    <div>
        <Banar/>
        <section class="py-4">
            <div class="container mx-auto">
                <Products/>
            </div>
        </section>
    </div>
</template>
<script setup>
import { ref } from 'vue'


const products = ref([])

const { data, error } = await useFetch('https://dummyjson.com/products', {
  params: { limit: 10, skip: 10, select: 'title,price,thumbnail,discountPercentage,brand', },
})

if (data.value && data.value.products) {
  products.value = data.value.products
}

if (error.value) {
  console.error('Failed to fetch products:', error.value)
}
const calculateOriginalPrice = (price, discountPercentage) => {
return price / (1 - discountPercentage / 100)
}
</script>