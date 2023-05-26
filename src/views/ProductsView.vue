<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <ProductCard v-for="(product, idx) in inventory" :key="product.id" :product="product" :addToCart="addToCart" :idx="idx"/>
    </div>
  </main>
</template>

<script>

import ProductCard from '../components/ProductCard.vue'

export default {
  props: ['inventory', 'addToCart'],
  components: {
    ProductCard
  },
}

</script>