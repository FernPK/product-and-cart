<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <button @click="toggle" class="cart-close">&times;</button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(quantity, key, idx) in cart" :key=key>
              <td><i class="icofont-3x"></i></td>
              <td>{{ key }}</td>
              <td>${{ getPrice(key) }}</td>
              <td class="center">{{ quantity }}</td>
              <td>${{ calculatePrice(key) }}</td>
              <td class="center">
                <button @click="remove(key)" class="btn btn-light cart-remove">
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p class="center" v-if="!Object.keys(this.cart).length"><em>No items in cart</em></p>
        <div class="spread">
          <span><strong>Total:</strong> ${{ calculateTotal() }}</span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>

export default {
  props: ['toggle','cart','inventory','remove'],
  methods: {
    getPrice(name){
      const product = this.inventory.find(item => item.name === name);
      return (product.price.USD).toFixed(2);
    },
    calculatePrice(name) {
      return (this.getPrice(name) * this.cart[name]).toFixed(2);
    },
    calculateTotal() {
      // let total = 0;
      // for (let key in this.cart) {
      //   total += this.calculatePrice(key);
      // }
      // const names = Object.keys(this.cart);
      // const total = Object.values(this.cart).reduce((acc, cur, index) => { // acc: accumulator, cur: current
      //   return acc + (cur * this.getPrice(names[index]));
      // }, 0);
      // console.log(this.cart);
      const total = Object.entries(this.cart).reduce((acc, [name, quantity]) => {
        return acc + (quantity * this.getPrice(name));
      }, 0);
      // console.log(total);
      return total.toFixed(2);
    },
  },
  updated() {
    for(let i = 0; i < Object.keys(this.cart).length; i++) {
      let icon;
      this.inventory.forEach(item => {
        if(item.name === Object.keys(this.cart)[i]){
          icon = item.icon;
        }
      });
      // console.log(icon);
      document.getElementsByClassName('icofont-3x')[i].classList.add(`icofont-${icon}`);
    }
  },
  mounted(){
    for(let i = 0; i < Object.keys(this.cart).length; i++) {
      let icon;
      this.inventory.forEach(item => {
        if(item.name === Object.keys(this.cart)[i]){
          icon = item.icon;
        }
      });
      // console.log(icon);
      document.getElementsByClassName('icofont-3x')[i].classList.add(`icofont-${icon}`);
    }
  }
}

</script>