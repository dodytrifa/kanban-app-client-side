<template>
  <div class="d-flex flex-column min-vh-100 justify-content-center align-items-center" style="background-color: #DBECFF">
      <form @submit.prevent="register" id="register-form">
        <h3 class="text-center mb-4">Register account</h3>
        <div class="mb-3 text-center">
          <label for="email" class="form-label">Email address</label>
          <input
            v-model="registerEmail"
            type="email"
            class="form-control"
            id="register-email"
            aria-describedby="emailHelp"
          />
        </div>
        <div class="mb-3 text-center">
          <label for="password" class="form-label">Password</label>
          <input
            v-model="registerPassword"
            type="password"
            class="form-control"
            id="register-password"
          />
        </div>

        <button type="submit" id="register" class="btn btn-primary">
          Create account
        </button>
        <button
          @click.prevent="directPage2"
          type="button"
          id="back"
          class="btn btn-secondary"
        >
          Back to login
        </button>
        <br />
        <p style="color: red" v-if="isRegisterError">{{ isRegisterError }}</p>
        <p style="color: blue" v-if="isRegisterSuccess">
          {{ isRegisterSuccess }}
        </p>
        <p style="color: black" v-if="isLoadingReg">Loading...</p>
        <br /><br />
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
      page: "register",
      isRegisterError: "",
      isRegisterSuccess: "",
      isLoadingReg: false,
    };
  },
  methods: {
    directPage2() {
      this.$emit("emitDirectPage", "login");
    },
    register() {
      this.isLoadingReg = true;
      setTimeout(() => {
        axios({
          method: "POST",
          url: `${this.urlServer}/users/register`,
          data: {
            email: this.registerEmail,
            password: this.registerPassword,
          },
        })
          .then((response) => {
            // console.log(response.data.msg);
            this.isLoadingReg = false;
            this.isRegisterSuccess = response.data.msg;
            this.registerEmail = "";
            this.registerPassword = "";
            this.isRegisterError = "";
          })
          .catch((err) => {
            this.isLoadingReg = false;
            console.log(err.response.data.errors);
            if (this.registerPassword.length < 6) {
              this.isRegisterError = err.response.data.errors;
            } else {
              this.isRegisterError = err.response.data.errors;
            }
          });
      }, 4000);
    },
  },
};
</script>

<style>
</style>