<template>
  <div class="d-flex align-items-center justify-content-center">
    <div class="d-flex justify-content-center">
      <div>
        <form @submit.prevent="login" id="login-form">
          <h1>Welcome to Kanban App</h1>
          <br />
          <h3>Please Login</h3>
          <br />
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label"
              >Email address</label
            >
            <input
              v-model="loginEmail"
              type="email"
              class="form-control-login"
              aria-describedby="emailHelp"
            />
          </div>
          <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label"
              >Password</label
            >
            <input
              v-model="loginPassword"
              type="password"
              class="form-control-login"
            />
          </div>

          <button type="submit" class="btn btn-primary">Submit</button
          ><br /><br />
          <p>If you don't have any account, please create an account</p>
          <div class="to-register-page" id="toRegister" style="cursor: pointer">
            <button
              @click.prevent="directPage"
              type="button"
              class="btn btn-outline-primary"
            >
              Create account
            </button>
          </div>

          <br />
        </form>
        <p style="color: red" v-if="isLoginError">{{ isLoginError }}</p>
      </div>
    </div>
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
      page: "login",
      isLoginError: "",
    };
  },
  methods: {
    directPage() {
      this.$emit("emitDirectPage", "register");
    },
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
          this.isLoginError = "";
          this.$emit("emitChangeLogin", true);
        })
        .catch((err) => {
          console.log(err.response.data);
          this.isLoginError = err.response.data;
        });
    },
  },
};
</script>

<style>
</style>