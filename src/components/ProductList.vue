<template>
  <div>
    <h1>Product List</h1>
    <img
      v-if="loading"
      src="load.gif"
      alt="loading..."
    />

    <ul v-else>
      <li
        v-for="product in products"
        :key="product.id"
      >
        {{ product.title }} - {{ product.price | currency }} - Quantity: {{ product.inventory }}
        <button @click="addProductToCart(product)">Add to cart</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: false
    }
  },
  computed: {
    // get array of the product from state
    products () {
      return this.$store.getters.avaliableProducts
    }
  },

  methods: {
    addProductToCart (product) {
      this.$store.dispatch('addProductToCart', product);
    }
  },

  created() {
    // set properties to the products by computed
    this.loading = true;
    this.$store.dispatch('fetchProducts')
      .then(() => this.loading = false);
  }
}
</script>

<style scoped>

</style>
