<template>
  <div v-if="products">
    <h2>Products</h2>
    <div class="products-container">
      <router-link v-for="product of products" :key="product.post_id" :to="{ name: 'ProductDetails', params: { id: product.post_id } }">
        <img :src="product.post_img" alt="">
        {{ product.post_title }}
        {{ product.post_category }}
        {{ product.post_price }}
      </router-link>
    </div>
  </div>
  <div v-else>Loading products...</div>
</template>
<script>
export default {
  data() {
    return {
      products: null,
    };
  },
  mounted() {
    // Fetch goes here
  },
};
</script>
<style>
.products-container {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin-inline: auto;
  padding: 30px;
  gap: 2%;
  justify-content: stretch;
  align-items: stretch;
  flex-direction: column;
}
</style>
