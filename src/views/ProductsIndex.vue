<template>
  <div class="products-index">

    <h1>All Products</h1>
    <div>
      Filter Name: <input v-model="nameFilter" list="names">

      <datalist id="names">
        <option v-for="product in products">{{ product.name }}</option>  
      </datalist>
    </div>

    <div v-for="product in filterBy(products, nameFilter, 'name')">
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
import Vue2Filters from "vue2-filters";

export default {
  data: function() {
    return {
      products: [],
      currentProduct: {},
      nameFilter: ''
    };
  },
  created: function() {
    axios.get('/api/products')
    .then(response => {
      this.products = response.data;
    });
  },
  methods: {},
  mixins: [Vue2Filters.mixin]
};
</script>
