<template>
    <button @click="addProductToCart(product)" class="flex items-center w-full text-center my-2 justify-center text-[14px] gap-3 border hover:bg-[#03A629] border-[#fff] rounded-[6px] py-[6px] px-[12px] bg-[#00000050] text-white "><img src="~/assets/icon/Vector.svg" alt=""> Add to Cart  <span v-if="productQuantity > 0">{{ productQuantity }}</span></button>
</template>
 
  <script setup>
  import { useCartStore } from '~/store/cart'
  import { ref } from 'vue'
  import { defineProps } from 'vue';

    const props = defineProps({
    product: {
        type: Object,
        required: true,
    },
    });
  const cartStore = useCartStore()
  const addProductToCart = (product) => {
    console.log('Add to cart button clicked', product);
    cartStore.addToCart(product)
  }
  // Create a computed property to get the quantity of the current product in the cart
const productQuantity = computed(() => {
  const item = cartStore.items.find((item) => item.id === props.product.id);
  return item ? item.quantity : 0;
});
  </script>
  