<template>
    <div class="container mx-auto p-4">
      <h1 class="text-3xl font-bold mb-6">Your Shopping Cart</h1>
      <div v-if="cartItems.length === 0" class="text-center">
        <p class="text-gray-500">Your cart is empty!</p>
        <router-link to="/" class="text-blue-500 hover:underline">Continue Shopping</router-link>
      </div>
      <div v-else>
        <div class="bg-white shadow-md rounded-lg overflow-hidden">
          <ul>
            <li v-for="item in cartItems" :key="item.id" class="flex items-center justify-between p-4 border-b">
              <div class="flex items-center">
                <img :src="item.thumbnail" alt="Product Image" class="h-16 w-16 object-cover rounded-md" />
                <div class="ml-4">
                  <h2 class="text-lg font-semibold">{{ item.name }}</h2>
                  <p class="text-gray-500">Price: ${{ item.price }}</p>
                  <div class="flex items-center mt-2">
                    <button @click="decreaseQuantity(item.id)" class="px-2 py-1 border rounded-lg text-gray-700 hover:bg-gray-100">-</button>
                    <span class="mx-2">{{ item.quantity }}</span>
                    <button @click="increaseQuantity(item.id)" class="px-2 py-1 border rounded-lg text-gray-700 hover:bg-gray-100">+</button>
                  </div>
                </div>
              </div>
              <div>
                <button @click="removeFromCart(item.id)" class="text-red-500 hover:underline">Remove</button>
              </div>
            </li>
          </ul>
          <div class="p-4 flex justify-between">
            <h3 class="text-lg font-bold">Total: ${{ totalAmount }}</h3>
            <button @click="checkout" class="px-4 py-2 bg-green-600 text-white rounded-lg hover:bg-green-500">Proceed to Checkout</button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue';
  import { useCartStore } from '~/store/cart'; 
  import { useRouter } from 'vue-router'; 
  const cartStore = useCartStore();
  const cartItems = computed(() => cartStore.items);
  const router = useRouter(); 
  const totalAmount = computed(() => {
    return cartItems.value.reduce((total, item) => total + item.price * item.quantity, 0);
  });
  
  const removeFromCart = (productId) => {
    cartStore.removeFromCart(productId);
  };
  
  const increaseQuantity = (productId) => {
    const item = cartStore.items.find(item => item.id === productId);
    if (item) {
      item.quantity += 1; 
    }
  };
  
  const decreaseQuantity = (productId) => {
    const item = cartStore.items.find(item => item.id === productId);
    if (item && item.quantity > 1) {
      item.quantity -= 1; 
    } else if (item && item.quantity === 1) {
      removeFromCart(productId);
    }
  };
  
  const checkout = () => {
//    alert(66) 
  router.push('/checkout'); 
};
  </script>
  
  <style scoped>

  </style>
  