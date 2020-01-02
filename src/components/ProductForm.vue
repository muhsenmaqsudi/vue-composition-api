<template>
  <form id="product-form" @submit.prevent="saveProduct">
    <div class="form-group">
      <label for="title">Title</label>
      <input
        class="form-control"
        type="text"
        id="title"
        v-model="inputState.title"
      />
    </div>
    <div class="form-group">
      <label for="price">Price</label>
      <input
        class="form-control"
        type="number"
        min="0"
        step="0.01"
        id="price"
        v-model="inputState.price"
      />
    </div>
    <button type="submit" :disabled="!isValid">Save</button>
  </form>
</template>

<script>
import {
  ref,
  reactive,
  watch,
  computed,
  onMounted
} from "@vue/composition-api";
export default {
  props: {
    createProduct: {
      type: Function,
      required: true
    }
  },
  setup(props) {
    onMounted(() => {
      console.log("hiii");
    });

    const inputState = reactive({
      title: "",
      price: ""
    });
    const submitted = ref(false);

    // eslint-disable-next-line no-unused-vars
    const priceAsNumber = computed(() => {
      return parseFloat(inputState.price);
    });

    const isValid = computed(() => {
      let isValid = true;

      if (inputState.title.trim().length === 0) {
        isValid = false;
      }

      if (isNaN(priceAsNumber.value) || priceAsNumber.value <= 0) {
        isValid = false;
      }
      return isValid;
    });

    watch(() => {
      if (submitted.value) {
        inputState.title = "";
        inputState.price = "";
        submitted.value = false;
      }
    });

    const saveProduct = () => {
      props.createProduct(inputState.title, priceAsNumber.value);
      submitted.value = true;
    };

    return {
      inputState,
      saveProduct,
      isValid
    };
  }
};
</script>

<style scoped>
.product-form {
  border: 1rem;
}
button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
}
.form-control {
  display: block;
  width: 100%;
  height: 34px;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  color: #555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.form-group {
  width: 33%;
  margin: 20px 30%;
  text-align: left;
}
</style>
