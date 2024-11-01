<template>
    <div>
        <header class="bg-white border-b shadow-md">
  <div class="container mx-auto px-6 py-4 flex items-center justify-between">
    

    <div class="flex items-center space-x-2">
      <nuxt-link to="/"  class="text-2xl font-bold text-gray-800"> ShopLogo </nuxt-link>
    </div>


    <div class="w-full max-w-lg mx-4 hidden lg:flex">
      <input 
        type="text" 
        placeholder="Search products..." 
        class="w-full border border-gray-300 rounded-full px-4 py-2 text-gray-700 focus:outline-none focus:border-indigo-500"
      />
    </div>


    <Category/>


    <div class="flex items-center space-x-4">
      <span  class="text-gray-700 hover:text-indigo-500 hidden cursor-pointer md:block">Account</span>
      <nuxt-link to="/cart" class="relative">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-700 hover:text-indigo-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4m0 0L4 4H2m16 12a2 2 0 11-4 0 2 2 0 014 0zm-6 0a2 2 0 11-4 0 2 2 0 014 0z"/>
        </svg>
        <span 
        v-if="cartCount > 0" 
        class="absolute top-[-5px] right-[-24px] inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-red-100 bg-red-600 rounded-full">
        {{ cartCount }}
      </span>
      </nuxt-link>
    </div>
  </div>
</header>

    </div>
</template>

<script setup>
import { computed } from 'vue';
import { useCartStore } from '~/store/cart';

const cartStore = useCartStore();

const cartCount = computed(() => cartStore.cartCount);
</script>