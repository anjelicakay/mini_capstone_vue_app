<template>
  <div class="product-new">
    <h1>New Recipe</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
    <form v-on:submit.prevent="submit()">
      <div>
        Name: <input v-model="newProductName">
      </div>
      <div>
        Decription: <input v-model="newProductDescription">
      </div>
      <div>
        Price: <input v-model="newProductPrice">
      </div>
      <div>
        Image: <input v-model="newProductImageUrl">
      </div>
      <input type="submit" value="Create" class="btn btn-warning">
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
      newProductName: "",
      newProductDescription: "",
      newProductPrice: "",
      newProductImageUrl: "",
      errors: []
    };
  },
  created: function() {},
  methods: {
    submit: function (){
      console.log("Create the Product..");
      var params={
                  name: this.newProductName,
                  description: this.newProductDescription,
                  price: this.newProductPrice,
                  image_url: this.newProductImageUrl
                  };
      axios.post("/api/products", params)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/");
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>