<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <h2>Make a new product</h2>
    <p>Name:<input type="text" v-model="name"></p>
    <p>Price:<input type="text" v-model="price"></p>
    <p>Description:<input type="text" v-model="description"></p>
    <p>Image_url:<input type="text" v-model="image_url"></p>
    <button v-on:click="createProduct()">Create Product</button>
    <br>
  

    <!-- <h2>{{ products }}</h2> -->
    <!-- <button v-on:click="productsIndex()">Show Products</button> -->
    <div v-for="product in products">
      {{ product.id }}
      {{ product.name }}
      <!-- {{ product.image_url }} -->
      <p><img v-bind:src="product.image_url" v-bind:alt="product.name"></p>
      <button v-on:click="showProduct(product)">Show more information</button>
      <hr>
    </div>
    <dialog id="product-details">
      <form method="dialog">
        <h3>Product information</h3>
        <p><strong>Name: </strong> <input type="text" v-model="currentProduct.name"></p>
        <p><strong>Price: </strong><input type="text" v-model="currentProduct.price"></p>
        <p><strong>Description: </strong><input type="text" v-model="currentProduct.description"></p>
        <p><strong>Image_url: </strong><input type="text" v-model="currentProduct.image_url"></p>
        <button>Close</button>
        <button v-on:click="updateProduct()">Update</button>
        <button v-on:click="destroyProduct()">Remove Product</button>
      </form>
    </dialog>  
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
      currentProduct: {},
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
    updateProduct: function () {
      var params = {
        name: this.currentProduct.name,
        price: this.currentProduct.price,
        description: this.currentProduct.description,
        image_url: this.currentProduct.image_url,
      };
      console.log("updating product..");
      axios
        .patch("/api/products/" + this.currentProduct.id, params)
        .then((response) => {
          console.log(response.data);
        });
    },
    showProduct: function (Product) {
      console.log("Product");
      this.currentProduct = Product;
      console.log("show product...");
      document.querySelector("#product-details").showModal();
    },
    destroyProduct: function () {
      console.log("destroy product...");
      axios
        .delete("/api/products/" + this.currentProduct.id)
        .then((response) => {
          console.log(response.data);
          var index = this.products.indexOf(this.currentProduct);
          console.log(index);
          this.products.splice(index, 1);
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