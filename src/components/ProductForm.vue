<template>
  <form id="product-form" @submit.prevent="saveProduct">
    <div class="form-group">
      <label for="title">Title</label>
      <input class="form-control" type="text" id="title" v-model="titleInput" />
    </div>
    <div class="form-group">
      <label for="price">Price</label>
      <input
        class="form-control"
        type="number"
        min="0"
        step="0.01"
        id="price"
        v-model="priceInput"
      />
    </div>
    <button type="submit" :disabled="!isValid">Save</button>
  </form>
</template>

<script>
export default {
  props: {
    createProduct: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      titleInput: "",
      priceInput: "",
      submitted: false
    };
  },
  computed: {
    price() {
      return parseFloat(this.priceInput);
    },
    isValid() {
      let isValid = true;

      if (this.titleInput.trim().length === 0) {
        isValid = false;
      }

      if (isNaN(this.price) || this.price <= 0) {
        isValid = false;
      }
      return isValid;
    }
  },
  watch: {
    submitted() {
      if (this.submitted) {
        this.titleInput = "";
        this.priceInput = "";
        this.submitted = false;
      }
    }
  },
  methods: {
    saveProduct() {
      this.createProduct(this.titleInput, this.price);
      this.submitted = true;
    }
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
