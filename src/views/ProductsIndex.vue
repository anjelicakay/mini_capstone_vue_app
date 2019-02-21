<template>
  <div class="products-index">

    <h1>All Products</h1>
    <div v-for="product in products">
      <h2>{{ product.name }}</h2>
      <router-link v-bind:to="'/products/' + product.id">
      <img v-bind:src="product.image_url" v-bind:alt="product.name">
      </router-link>  
    </div>
  </div>
</template>

<style>
  img{
    width: 250px;
  }
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      products: [],
      currentProduct: {}
    };
  },
  created: function() {
    axios.get('/api/products')
    .then(response => {
      this.products = response.data;
    });
  },
  methods: {}
};
</script>
