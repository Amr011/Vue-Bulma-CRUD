<template>
  <div>
    <router-link :to="{ name: 'Create' }" class="button is-success mt-5">Add New</router-link>
    <table class="table is-striped is-bordered mt-2 is-fullwidth">
      <thead>
        <tr>
          <th>Product Name</th>
          <th>Price</th>
          <th class="has-text-centered">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.product_id">
          <td>{{ item.product_name }}</td>
          <td>{{ item.product_price }}</td>
          <td class="has-text-centered">
            <router-link
              :to="{ name: 'Edit', params: { id: item.product_id } }"
              class="button is-info is-small is-rounded">Edit</router-link>
              
             <a class="button is-danger is-small is-rounded ml-1"
              @click="deleteProduct(item.product_id)">Delete</a>
              
          </td>
        </tr>
      </tbody>
    </table>
<ProductDetails/>

  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 import ProductComp from "../components/ProductComp.vue"
export default {
  name: "ProductList",
  components:ProductComp,
  data() {
    return {
      items: [],
    };
  },
 
  created() {
    this.getProducts();
  },
 
  methods: {
    // Get All Products
    async getProducts() {
      try {
        const response = await axios.get("http://localhost:7000/products");
        this.items = response.data;
      } catch (err) {
        console.log(err);
      }
    },
 
    // Delete Product
    async deleteProduct(id) {
      try {
        await axios.delete(`http://localhost:7000/products/${id}`);
        this.getProducts();
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
 
<style>
</style>