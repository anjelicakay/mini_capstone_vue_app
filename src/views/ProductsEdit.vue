<template>
  <div class="products-edit">
    <h1>Edit Product</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
      <div>
        Name: <input v-model="product.name">
      </div>
      <div>
        Decription: <input v-model="product.description">
      </div>
      <div>
        Price: <input v-model="product.price">
      </div>
      <div>
        Image: <input v-model="product.image_url">
      </div>
      <input type="submit" value="Update" class="btn btn-warning">
    </form>

  </div>
</template>

<style>
</style>

<script>
var axios = require('axios')

export default {
  data: function() {
    return {
      product: {
              id: "",
              name: "",
              description: "",
              image_url: "",
              price: "",
              tax: "",
              total: "",
              },
      errors: []        
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id)
      .then(response => {
        console.log(response.data);
        this.product = response.data;
      });
  },
  methods: {
    submit: function() {
      var params = {
                    name: this.product.name,
                    description: this.product.description,
                    price: this.product.price,
                    image_url: this.product.image_url
                  };
      axios.patch("/api/products/" + this.product.id, params)
        .then(response => {
          this.$router.push("/products/" + this.product.id);
        }).catch(error => {
          this.errors = error.response.data.errors;
        });           
    }
  }
};
</script>