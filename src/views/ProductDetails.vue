<template>
  <div v-if="product">
    <div class="product">
      <img
        class="product-image neu-border"
        :src="product.post_img"
        :alt="product.post_title"
      />
      <div class="product-details">
        <h2>{{ product.post_title }}</h2>
        <h4>{{ product.post_date }}</h4>
        <p>{{ product.post_body }}</p>
      </div>
    </div>
  </div>
  <div v-else>Loading the product...</div>
</template>
<script>
// import productCard from "@/components/products/productCard.vue";

export default {
  // components: { productCard },
  props: ["id"],
  data() {
    return {
      product: null,
    };
  },
  mounted() {
    // Fetch goes here
  },
};
</script>
<style>
.product {
  display: flex;
  padding: 0 10%;
  /* max-width: 600px; */
  margin-inline: auto;
  align-items: stretch;
  gap: 30px;
}
.product-image {
  padding: 10px;
  width: 50%;
  max-height: 80vh;
  object-fit: contain;
}
.product-details {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: center;
  text-align: end;
  gap: 8px;
}

.products-container {
  display: flex;
  flex-wrap: wrap;
  /* max-width: 600px; */
  width: 100%;
  margin-inline: auto;
  padding: 30px;
  /* overflow: auto; */
  gap: 2%;
  justify-content: stretch;
  align-items: stretch;
}
.neu-border {
  border-radius: 30px;
  background: #f5f5f5;
  box-shadow: 8px 8px 15px #e4e4e4, -8px -8px 15px #ffffff;
}
.neu-border-inset {
  border-radius: 30px;
  background: #f5f5f5;
  box-shadow: inset 8px 8px 15px #e4e4e4, inset -8px -8px 15px #ffffff;
}
@media screen and (max-width: 500px) {
  .product {
    flex-direction: column;
  }
  .product-image,
  .product-details {
    width: 100%;
  }

  .product-details {
    align-items: flex-start;
    text-align: left;
  }
}
</style>
