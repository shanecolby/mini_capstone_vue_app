<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <h2>Make a new product</h2>
    <p>Name:<input type="text" v-model="name"></p>
    <p>Price:<input type="text" v-model="price"></p>
    <p>Description:<input type="text" v-model="description"></p>
    <p>Image_url:<input type="text" v-model="image_url"></p>
    <button v-on:click="createProduct()">Create Product</button>

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
      products: [],
      name: "",
      price: "",
      description: "",
      image_url: "",
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
    createProduct: function () {
      console.log("creating product..");
      var params = {
        name: this.name,
        price: this.price,
        description: this.description,
        image_url: this.image_url,
      };
      axios.post("/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
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