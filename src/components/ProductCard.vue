<template>
  <div class="card">
    <div class="card-title">
      {{ product.name }}
    </div>
    <div class="card-body">
      <i class="icofont-10x" ></i>
      <form>
        <div class="row">
          <div class="cell">
            <label>Type:</label>
          </div>
          <div class="cell">
            <em>{{ product.type }}</em>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Price:</label>
          </div>
          <div class="cell">
            ${{ (product.price.USD).toFixed(2) }}
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Quantity:</label>
          </div>
          <div class="cell">
            <input type="number" v-model.number="product.quantity" min="0">
          </div>
        </div>
      </form>
    </div>
    <div class="card-footer">
      <button @click="addToCart(product.name, idx)" class="btn btn-light">
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>

export default {
  props: ['product', 'idx', 'addToCart'],
  mounted() {
    document.getElementsByClassName('icofont-10x')[this.idx].classList.add(`icofont-${this.product.icon}`)
  },
}

</script>