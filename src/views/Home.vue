<template>

<section>
  <div class="hello">
    <h1>Kicking n Screaming</h1>
  </div>
  <p>
    We are an e-commerce business selling soccer gear. Blah blah blah
  </p>

<button type="button" class="btn btn-primary btn-lg"><router-link :to="{ name: 'Login' }">Log in</router-link></button>
<button type="button" class="btn btn-secondary btn-lg"><router-link :to="{ name: 'Register' }">Sign up</router-link></button>
</section>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    login() {
      console.log(this.email, this.password);
      fetch("http://localhost:2000/users", {
      method: "PATCH", 
      body: JSON.stringify({
        email: this.email, 
        password: this.password
        }), 
        headers: {
        "Content-Type": "application/json; charset=UTF-8"
        },
        })
        .then((response) => response.json())
        .then((json) => alert(json))
        .catch((e) => alert(e.msg))
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

section{
    height: 100vh;
    background-image: url('https://picsum.photos/1920/1080');
}

.hello{
  padding-top: 200px

}

h1{
  color: blue;
  font-size: 100px;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: rgb(0, 195, 255);
  text-decoration: none;
}
button {
  margin: 10px;
}



</style>
