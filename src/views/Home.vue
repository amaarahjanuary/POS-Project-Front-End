<template>

<section>
  <div class="hello">
    <h1>Kicking n Screaming</h1>
  </div>
  <p>
    We are an e-commerce business selling soccer gear. Blah blah blah
  </p>
    <form @submit.prevent="login" class="form neu-border">
    <h2 class="form-heading">Login</h2>
    <input
      class="form-input neu-border-inset"
      type="email"
      v-model="email"
      placeholder="Email"
    />
    <input
      class="form-input neu-border-inset"
      type="password"
      v-model="password"
      placeholder="Password"
    />
    <button type="submit" class="form-btn neu-border">Sign in</button>
    <div class="form-social-login">
      <button class="form-btn neu-border form-social-btn">
        <i class="fab fa-google"></i>
      </button>
      <button class="form-btn neu-border form-social-btn">
        <i class="fab fa-facebook-f"></i>
      </button>
    </div>

    <p>
      Not a member?
      <router-link :to="{ name: 'Register' }">Create an account</router-link>
    </p>
  </form>
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
  color: blue;
}

form{
  margin-top: 100px;
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

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 40px;
  gap: 20px;
  width: 100%;
  margin-inline: auto;
  max-width: 600px;
}

.form-heading {
  text-align: center;
  text-transform: uppercase;
}

.form-input,
.form-btn {
  border: none;
  line: none;
  padding: 20px;
}

.form-btn {
  cursor: pointer;
  transition: all 0.1s linear;
}

.form-btn:hover {
  transform: scale(1.05);
}

.form-social-login {
  display: flex;
  justify-content: space-between;
}

.form-social-btn {
  width: 45%;
  color: #333;
}
</style>
