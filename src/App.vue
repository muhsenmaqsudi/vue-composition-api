<template>
  <div id="app">
    <div id="user-info">
      <button @click="toggleUserInfo">
        {{ showUserInfo ? "Hide" : "Show" }} User Details
      </button>
      <p v-if="showUserInfo">You're logged in!</p>
    </div>
    <product-form :createProduct="createProduct" />
    <products :items="products" :remove="deleteProduct" />
  </div>
</template>

<script>
import ProductForm from "./components/ProductForm";
import Products from "./components/Products";

export default {
  name: "app",
  components: {
    ProductForm,
    Products
  },
  data() {
    return {
      products: [],
      showUserInfo: false
    };
  },
  methods: {
    createProduct(title, price) {
      const newProduct = {
        id: Math.random(),
        title: title,
        price: price
      };

      this.products.push(newProduct);
    },
    deleteProduct(productId) {
      this.products = this.products.filter(p => p.id !== productId);
    },
    toggleUserInfo() {
      this.showUserInfo = !this.showUserInfo;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  background-color: #0e67ec;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
}
</style>
