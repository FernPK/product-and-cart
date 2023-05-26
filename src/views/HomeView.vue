<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <div class="splash-container">
    <div class="splash">
      <h1>Splendid Food</h1>
    </div>
  </div>

  <main class="wrapper">

    <h2>Recommended</h2>

    <div class="recommended">

      <ProductCard v-for="(product, idx) in inventory.slice(0,3)" :key="product.id" :product="product" :addToCart="addToCart" :idx="idx"/>

    </div>

  </main>
</template>

<script>
  import ProductCard from '../components/ProductCard.vue'
  export default {
    // name: 'HomeView',
    props: ['inventory', 'addToCart'],
    components: {
      ProductCard,
    },
    // data() {
    //   return {
    //     inventory: food,
    //     cart: []
    //   }
    // },
    // methods: {
      // addToCart(name, idx) {
      //   this.cart.push(name)
      //   this.inventory[idx].quantity--
      // }
    // }
  }
</script>