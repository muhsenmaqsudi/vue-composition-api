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
import { ref } from "@vue/composition-api";
import ProductForm from "./components/ProductForm";
import Products from "./components/Products";
import { useToggle } from "./cmp-functions/toggle";

export default {
  name: "app",
  components: {
    ProductForm,
    Products
  },
  setup() {
    const products = ref([]);
    // let showUserInfo = reactive({ show: false });
    const createProduct = (title, price) => {
      const newProduct = {
        id: Math.random(),
        title: title,
        price: price
      };

      products.value.push(newProduct);
    };

    const deleteProduct = productId => {
      products.value = products.value.filter(p => p.id !== productId);
    };

    // const showUserInfo = ref(false);

    // const toggleUserInfo = () => {
    //   showUserInfo.value = !showUserInfo.value;
    // };

    const { show: showUserInfo, toggle: toggleUserInfo } = useToggle();

    return {
      products,
      showUserInfo,
      createProduct,
      deleteProduct,
      toggleUserInfo
    };
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
