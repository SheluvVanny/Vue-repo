<template>
  <div id="app">
    <ProductList @addToCart="addToCart" />
    <Cart :cart="cart" @removeFromCart="removeFromCart" />
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import Cart from "./components/Cart.vue";

export default {
  components: { ProductList, Cart },
  data() {
    return {
      cart: [],
    };
  },
  methods: {
    addToCart(product) {
      const existing = this.cart.find((item) => item.id === product.id);
      if (existing) {
        existing.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(item) {
      const index = this.cart.indexOf(item);
      if (index !== -1) {
        this.cart.splice(index, 1);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
