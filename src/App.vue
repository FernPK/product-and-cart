<script setup>
import { RouterLink, RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <RouterLink to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </RouterLink>
      <RouterLink to="/products" class="top-bar-link">
        <span>Products</span>
      </RouterLink>
      <RouterLink to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </RouterLink>
    </nav>
    <div @click="toggleSideBar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </div>

    <!-- <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" /> -->

    <!-- <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
      
    </div> -->
  </header>

  <RouterView :inventory="inventory" :addToCart="addToCart"/>

  <Sidebar 
    v-if="showSideBar" 
    :toggle="toggleSideBar"
    :cart="cart"
    :inventory="inventory"
    :remove="remove"
  />

</template>

<script>

// import Sidebar from './components/Sidebar.vue'
import Sidebar from '@/components/Sidebar.vue'
import food from './food.json'

export default {
  components: {
    Sidebar
  },
  // setup() {
  //   return {
  //     toggleSideBar() {
  //       console.log('toggleSideBar')
  //     }
  //   }
  // }
  data() {
    return {
      showSideBar: false,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity() {
      // let total = 0;
      // for (let key in this.cart) {
      //   total += this.cart[key];
      // }
      // return total;
      // Object.values(this.cart).forEach(quantity => total += quantity);
      return Object.values(this.cart).reduce((acc, cur) => acc + cur, 0);
    }
  },
  methods: {
    addToCart(name, index) {
      if (!this.cart[name]) {
        this.cart[name] = 0;
      }
      this.cart[name] += this.inventory[index].quantity;
      this.inventory[index].quantity = 0;
      // console.log(this.cart)
    },
    toggleSideBar() {
      this.showSideBar = !this.showSideBar
    },
    remove(name) {
      delete this.cart[name];
    }
  },
  // async mounted() {
  //   const res = await fetch('./food.json');
  //   const data = await res.json();
  //   this.inventory = data;
  // }
}

</script>

<style scoped>
/* header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
} */
</style>
