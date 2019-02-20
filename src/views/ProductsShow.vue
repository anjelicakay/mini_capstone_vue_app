<template>
  <div class="products-show">
    <h1>{{ product.name }}</h1>
    <h4>Description: {{ product.description }}</h4>
    <h4>Price: {{ product.price }}</h4>
    <h4>Image: {{ product.image_url }}</h4>
  </div>  
</template>

<style>
  
</style>

<script>
var axios = require('axios');

export default{
  data: function() {
    return {
      product: {

                }
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id)
      .then(response => {
        console.log(response.data);
        this.product = reponse.data;
      });
  },
  methods: {}
}  
</script>