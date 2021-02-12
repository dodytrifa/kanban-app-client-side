<template>
  <div class="d-flex justify-content-center">
    <form @submit.prevent="login" id="login-form">
      <h3>Login</h3>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">Email address</label>
        <input
          v-model="loginEmail"
          type="email"
          class="form-control-login"
          aria-describedby="emailHelp"
        />
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">Password</label>
        <input
          v-model="loginPassword"
          type="password"
          class="form-control-login"
        />
      </div>
      <div class="to-register-page" id="toRegister" style="cursor: pointer">
        <a>Click here to create account</a>
      </div>
      <br />

      <button type="submit" class="btn btn-primary">Submit</button><br /><br />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["dataisLogin", "urlServer"],
  data() {
    return {
      loginEmail: "",
      loginPassword: "",
    };
  },
  methods: {
    changePage() {},
    login() {
      axios({
        method: "POST",
        url: `${this.urlServer}/users/login`,
        data: {
          email: this.loginEmail,
          password: this.loginPassword,
        },
      })
        .then((response) => {
          console.log(response);
          localStorage.setItem("access_token", response.data.access_token);
          this.loginEmail = "";
          this.loginPassword = "";
          this.$emit("emitChangeLogin", true);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
</style>