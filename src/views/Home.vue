<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- <h2>{{ products }}</h2> -->
    <!-- <button v-on:click="productsIndex()">Show Products</button> -->
    <div v-for="product in products">
      {{ product.name }}
      <!-- {{ product.image_url }} -->
      <p><img v-bind:src="product.image_url" v-bind:alt="product.name"></p>
      <hr>
    </div>
  </div>
</template>
<style>
</style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Products Page",
      products: [
        // { id: 1, name: "Product 1", price: 10 },
        // { id: 2, name: "Product 2", price: 230 },
      ],
    };
  },

  created: function () {
    console.log("in created");
    this.productsIndex();
  },
  methods: {
    productsIndex: function () {
      console.log("products index..");
      axios.get("/api/products").then((response) => {
        console.log(response.data);
        this.products = response.data;
      });
    },
  },
};
</script>


//     console.log("in created");
//     this.productsIndex();
//     },
//     methods: {
//     productsIndex: function () {
//       console.log("products index..");
//       axios.get("/api/products").then((response) => {
//         console.log(response.data);
//         this.products = response.data;
//       });
//     },
//   },
// };
// </script>