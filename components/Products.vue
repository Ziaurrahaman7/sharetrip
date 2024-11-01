<template>
    <div class="grid lg:grid-cols-5 grid-cols-2 md:grid-cols-4 p-3 gap-4">
      <div 
        v-for="(product, index) in products" 
        :key="index"
        class="bg-white rounded-lg relative hover:shadow-md my-3 product-card hover:border border-white h-[332px] overflow-hidden"
      >
        <!-- Product Image -->
        <div>
          <ProductDiscount  :discountPercentage="product.discountPercentage"/>
          <ProductWishlist />
          <img 
            class="mx-auto min-w-[210px] max-h-[209px] object-cover" 
            :src="product.thumbnail || 'https://via.placeholder.com/300x200'" 
            alt="Product Image" 
          />
  
          <!-- Product Details -->
          <div class="py-2 px-3">
            <!-- Product Title -->
            <p class="mt-1 text-[#5A6573] text-[14px]">{{ product.brand }}</p>
            <h3 class="lg:text-[16px] text-[13px] mt-1 font-semibold text-[#1A2B3D]">
              {{ product.title }}
            </h3>
            <div class="flex items-center gap-4 mt-1">
              <!-- Product Price -->
              <span class="text-[20px] text-[#1882FF]">৳ {{ product.price }}</span>     
              <span class="text-[14px] line-through text-[#77818C]"> ৳ {{ calculateOriginalPrice(product.price, product.discountPercentage).toFixed(2) }}</span> <!-- Assuming a dummy old price -->
            </div>
          </div>
  
          <!-- Overlay with Actions -->
          <div class="absolute button-area top-[30%] w-full px-4">
            <ProductAddtocart :product="product"/>
            <ProductQuickview />
          </div>
        </div>
      </div>
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
  
  <style scoped>
  .button-area {
    display: block;
    opacity: 0;
    transform: translateY(10px);
    transition: opacity 0.3s ease, transform 0.3s ease;
  }
  
  .product-card:hover .button-area {
    opacity: 1;
    transform: translateY(0);
  }
  </style>
  