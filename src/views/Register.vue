<template>
  <div class="d-flex justify-content-center">
    <form @submit.prevent="register" id="register-form">
      <h3>Register</h3>
      <div class="mb-3">
        <label for="email" class="form-label">Email address</label>
        <input
          v-model="registerEmail"
          type="email"
          class="form-control"
          id="register-email"
          aria-describedby="emailHelp"
        />
      </div>
      <div class="mb-3">
        <label for="password" class="form-label">Password</label>
        <input
          v-model="registerPassword"
          type="password"
          class="form-control"
          id="register-password"
        />
      </div>

      <div class="backtologin" id="toLogin" style="cursor: pointer">
        <a>Back to Login</a><br /><br />
      </div>

      <button type="submit" id="register" class="btn btn-primary">
        Create account</button
      ><br /><br />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["urlServer"],
  data() {
    return {
      registerEmail: "",
      registerPassword: "",
    };
  },
  methods: {
    register() {
      axios({
        method: "POST",
        url: `${this.urlServer}/users/register`,
        data: {
          email: this.registerEmail,
          password: this.registerPassword,
        },
      })
        .then((response) => {
          console.log(response.data.msg);
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