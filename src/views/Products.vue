<template>
  <div v-if="products">
    <h2>Products</h2>
    <div class="products-container" v-if="products">
      <router-link
        v-for="product of products"
        :key="product._id"
        :to="{ name: 'ProductDetails', params: { id: product._id } }"
      >
        <img :src="product.img" :alt="product.title" />
        {{ product.author_name }}
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
    if (localStorage.getItem("jwt")) {
      fetch("https://generic-blog-api.herokuapp.com/posts", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.products = json;
          this.products.forEach(async (product) => {
            await fetch(
              "https://generic-blog-api.herokuapp.com/users/" + blog.author,
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
                blog.author_name = json.name;
              });
          });
        })
        .catch((err) => {
          alert("User not logged in");
        });
    } else {
      alert("User not logged in");
      this.$router.push({ name: "Login" });
    }
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

img {
  max-width: 50vw;
}
</style>
