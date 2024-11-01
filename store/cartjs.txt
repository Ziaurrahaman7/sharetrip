// stores/cart.js
import { defineStore } from 'pinia'
// import { defineStore } from 'pinia'
export const useCartStore = defineStore('cart', {
  state: () => ({
    items: [],
  }),
  actions: {
    addToCart(product) {
      const item = this.items.find((item) => item.id === product.id)
      if (item) {
        item.quantity += 1
      } else {
        this.items.push({ ...product, quantity: 1 })
      }
    },
    removeFromCart(productId) {
      this.items = this.items.filter((item) => item.id !== productId)
    },
  },
  getters: {
    cartCount: (state) => state.items.reduce((count, item) => count + item.quantity, 0),
    cartTotal: (state) => state.items.reduce((total, item) => total + item.price * item.quantity, 0),
  },
})
