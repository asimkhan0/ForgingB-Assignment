<template>
  <div class="home">
    <div class="login-form">
      <input
        v-model="email"
        type="text"
        class="form-control"
        id="email"
        placeholder="Please enter your email"
      />

      <password
        v-model="password"
        type="password"
        class="form-control"
        id="password"
        width="auto"
      />

      <button @click="login" type="button" id="login" class="btn btn-success">
        Login
      </button>
      <div id="response"></div>
    </div>
  </div>
</template>

<script>
import Password from "vue-password-strength-meter";
var querystring = require("querystring");

import axios from "axios";
export default {
  name: "home",
  components: {
    Password
  },
  data() {
    return {
      email: "test001@gmaill.com",
      password: "Passworddd1"
    };
  },
  methods: {
    login() {
      // const formData = new FormData();
      // formData.append("email", this.email);
      // formData.append("password", this.password);
      // let config = {
      //   headers: {
      //     "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8"
      //   }
      // };
      // axios
      //   .post("http://api.forgingblock.io/signin", {
      //       email: this.email,
      //       password: this.password
      //     })
      //   .then(response => {
      //     console.log(response);
      //   });
      axios
        .post(
          "http://api.forgingblock.io/signin",
          querystring.stringify({
            username: this.email,
            password: this.password
          }),
          {
            headers: {
              "Content-Type": "application/x-www-form-urlencoded"
            }
          }
        )
        .then(function(response) {
          console.log(response);
        });
    }
  }
};
</script>

<style scoped>
input {
  background-color: #f1f1f1;
  border: 1px solid #f1f1f1;
  border-radius: 2px;
  box-sizing: border-box;
  font-size: 14px;
  padding: 13px;
  width: 400px;
  margin-bottom: 8px;
}
.login-form {
  width: 50%;
  margin: 0 auto;
}
</style>
