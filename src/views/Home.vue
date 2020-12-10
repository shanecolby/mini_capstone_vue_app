<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="product in Products">
      {{ product.name }}
      <hr>
    </div>
  </div>
</template>
<style>
</style>
<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      Products: [
        { id: 1, name: "Product 1", price: 10 },
        { id: 2, name: "Product 2", price: 230 },
      ]
      products: []
    };
  },
  created: function () {
    console.log('in created');
    this.productsIndex();
  },
  methods: {
    productsIndex: function(){
      console.log('products index..');
      axios.get('/api/products').then(response => {
        console.log(response.data);
        this.products = response.data;
      });
    }

  },
};
</script>