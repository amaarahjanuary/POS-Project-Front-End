<template>
    <div class="container d-flex justify-content-end mb-3 mt-5 pt-4">
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort by category</label>
        <select
          class="form-select"
          name=""
          id="sortCategory"
          onchange="sortCategory()"
        >
          <option value="All">All</option>
          <option value="Footwear">Footwear</option>
                <option value="Clothing">Clothing</option>
                <option value="Accessories">Accessories</option>
        </select>
      </div>
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort name</label>
        <select class="form-select" name="" id="sortName" onchange="sortName()">
          <option value="ascending">Ascending</option>
          <option value="descending">Descending</option>
        </select>
      </div>
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort price</label>
        <select
          class="form-select"
          name=""
          id="sortPrice"
          onchange="sortPrice()"
        >
          <option value="ascending">Ascending</option>
          <option value="descending">Descending</option>
        </select>
      </div>
    </div>
          <div class="card">
        <img src="${product.img}" class="card-img-top" alt="${product.title}">
        <div class="card-body">
          <h5 class="card-title">${product.title}</h5>
          <h5 class="card-category">${product.category}</h5>
          <p class="card-text">R${product.price}</p>
          <div class="d-flex mb-3">
            <input type="number" class="form-control" value=1 min=1 id="addToCart${position}">
            <button type="button" class="btn btn-secondary ms-3" onclick="addToCart(${position})"><i class="bi bi-bag-plus"></i></button>
          </div>
        </div>
          </div>
  <div v-if="products">
    <h2>Products</h2>
    <div class="products-container" v-if="products">
      <router-link
        v-for="product of products"
        :key="product._id"
        :to="{ name: 'ProductDetails', params: { id: product._id } }"
      >
        <img :src="product.img" :alt="product.title" />
        {{ product.category }}
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
      fetch("https://pos-backend-proj.herokuapp.com/products", {
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
              "https://pos-backend-proj.herokuapp.com/users" + product.title,
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
                product.title = json.name;
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
