<template>
    <div class="container mx-auto p-4">
      <h1 class="text-3xl font-bold mb-6">Checkout</h1>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <div class="bg-white shadow-md rounded-lg p-6">
          <h2 class="text-xl font-semibold mb-4">Shipping Information</h2>
          <form @submit.prevent="handleSubmit">
            <div class="mb-4">
              <label class="block text-gray-700 mb-2" for="name">Full Name</label>
              <input type="text" v-model="shippingInfo.name" id="name" required class="w-full border border-gray-300 rounded-lg p-2"/>
            </div>
            <div class="mb-4">
              <label class="block text-gray-700 mb-2" for="address">Address</label>
              <input type="text" v-model="shippingInfo.address" id="address" required class="w-full border border-gray-300 rounded-lg p-2"/>
            </div>
            <div class="mb-4">
              <label class="block text-gray-700 mb-2" for="city">City</label>
              <input type="text" v-model="shippingInfo.city" id="city" required class="w-full border border-gray-300 rounded-lg p-2"/>
            </div>
            <div class="mb-4">
              <label class="block text-gray-700 mb-2" for="state">State</label>
              <input type="text" v-model="shippingInfo.state" id="state" required class="w-full border border-gray-300 rounded-lg p-2"/>
            </div>
            <div class="mb-4">
              <label class="block text-gray-700 mb-2" for="zip">ZIP Code</label>
              <input type="text" v-model="shippingInfo.zip" id="zip" required class="w-full border border-gray-300 rounded-lg p-2"/>
            </div>
            <div class="mb-4">
              <label class="block text-gray-700 mb-2" for="phone">Phone Number</label>
              <input type="tel" v-model="shippingInfo.phone" id="phone" required class="w-full border border-gray-300 rounded-lg p-2"/>
            </div>
            <button type="submit" class="mt-4 w-full bg-green-600 text-white rounded-lg p-2 hover:bg-green-500">Continue to Payment</button>
          </form>
        </div>
        <div class="bg-white shadow-md rounded-lg p-6">
          <h2 class="text-xl font-semibold mb-4">Order Summary</h2>
          <div v-for="item in cartItems" :key="item.id" class="flex justify-between mb-4">
            <div>
            <div class="flex gap-4 items-center">
                <img :src="item.thumbnail" alt="Product Image" class="h-16 w-16 object-cover rounded-md" />
              <p class="font-semibold">{{ item.title }} (x{{ item.quantity }})</p>
            </div>
              <p class="text-gray-500">${{ item.price }} each</p>
            </div>
            <p class="font-semibold">${{ (item.price * item.quantity).toFixed(2) }}</p>
          </div>
          <div class="flex justify-between font-bold mb-4">
            <span>Total</span>
            <span>${{ totalAmount.toFixed(2) }}</span>
          </div>
        
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  import { useCartStore } from '~/store/cart'; 
  
  const cartStore = useCartStore();
  const cartItems = computed(() => cartStore.items);
  const totalAmount = computed(() => {
    return cartItems.value.reduce((total, item) => total + item.price * item.quantity, 0);
  });
  
  const shippingInfo = ref({
    name: '',
    address: '',
    city: '',
    state: '',
    zip: '',
    phone: ''
  });
  
  const handleSubmit = () => {
    console.log('Shipping Information:', shippingInfo.value);
   
  };
  
  const checkout = () => {
    console.log('Order placed successfully!');
  };
  </script>
  
  <style scoped>
 
  </style>
  