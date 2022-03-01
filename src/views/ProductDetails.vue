<template>
  <div v-if="product">
    <div class="product">
      <img class="product-image neu-border" :src="product.img" :alt="product.title" />
      <div class="product-details">
        <h2>{{ product.title }}</h2>
        <h4>{{ product.category }} - {{ product.price }}</h4>
        <p>{{ product.img }}</p>
      </div>
    </div>
  </div>
  <div v-else>Loading the product...</div>
</template>
<script>
export default {
  props: ["id"],
  data() {
    return {
      product: null,
    };
  },
  mounted() {
    fetch("https://generic-blog-api.herokuapp.com/posts/" + this.id, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then(async (json) => {
        this.product = json;
        await fetch(
          "https://generic-blog-api.herokuapp.com/users/" + json.title,
          {
            method: "GET",
            headers: {
              "Content-type": "application/json; charset=UTF-8",
              Authorization: `Bearer ${localStorage.getItem("jwt")}`,
            },
          }
        )
          .then((response) => response.json())
          .then((json) => {
            this.product.title = json.name;
          });
      });
  },
};
</script>
<style>
.product {
  display: flex;
  flex-direction: column;
  padding: 0 10%;
  margin-inline: auto;
  align-items: stretch;
  gap: 30px;
}
.product-image {
  padding: 10px;
  width: 100%;
  min-width: 100%;
  max-height: 50vh;
  object-fit: cover;
}
.product-details {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: left;
  gap: 8px;
}

.products-container {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin-inline: auto;
  padding: 30px;
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
