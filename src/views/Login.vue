<template>
  <div >
    <div class="d-flex justify-content-center">
      <div>
        <form @submit.prevent="login" id="login-form">
          <h1>Welcome to Kanban App</h1>
          <br />
          <div class="d-flex justify-content-center">
          <h3>Please Login</h3>
          </div>
          <br />
            <label for="exampleInputEmail1" class="form-label d-flex justify-content-center"
              >Email address</label
            >
          <div class="mb-3 d-flex justify-content-center">
            <input
              v-model="loginEmail"
              type="email"
              class="form-control-login"
              aria-describedby="emailHelp"
            />
          </div>
            <label for="exampleInputPassword1" class="form-label d-flex justify-content-center"
              >Password</label
            >
          <div class="mb-3 d-flex justify-content-center">
            <input
              v-model="loginPassword"
              type="password"
              class="form-control-login"
            />
          </div>
          <div class="d-flex justify-content-center">
          <button type="submit" class="btn btn-primary d-flex">Submit</button>
          </div>
          <br />
          
          <p class="text-center">If you don't have any account, please create an account</p>
          <div class="to-register-page d-flex justify-content-center" id="toRegister" style="cursor: pointer">
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
        <p class="d-flex justify-content-center" style="color: red" v-if="isLoginError">{{ isLoginError }}</p>
        <p class="d-flex justify-content-center" style="color: green" v-if="isLoadingLogin">Loading...</p>
      </div>
    </div>
    <div class="googlebutton">
    <GoogleLogin
    :params="params" 
    :renderParams="renderParams"
    :onSuccess="onSuccess"
    :onFailure="onFailure"
     ></GoogleLogin>
    </div>
  </div>
</template>

<script>

import GoogleLogin from "vue-google-login"
import axios from "axios";
export default {
  props: ["dataisLogin", "urlServer"],
  components: {
    GoogleLogin
  },
  data() {
    return {
      loginEmail: "",
      loginPassword: "",
      page: "login",
      isLoginError: "",
      isLoadingLogin: false,
      params: {
        client_id: "1029772264118-apmh4e72gci77pk1m8grvuobc6s1i2le.apps.googleusercontent.com"
      },
      renderParams: {
        width: 250,
        height: 50,
        longtitle: true
      },
    };
  },
  methods: {
    directPage() {
      this.$emit("emitDirectPage", "register");
    },
    login() {
      this.isLoadingLogin = true;
      setTimeout(() => {
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
            this.isLoadingLogin = false;
            this.$emit("emitChangeLogin", true);
          })
          .catch((err) => {
            console.log(err.response.data);
            this.isLoadingLogin = false;
            this.isLoginError = err.response.data;
          });
      }, 4000);
    },
    onSuccess (googleUser) {
      let id_token = googleUser.getAuthResponse().id_token
      axios({
        method: "POST",
        url: `${this.urlServer}/users/googlelogin`,
        data: {
          googleToken: id_token
        }
      })
        .then((response) => {
          console.log(response);
          // console.log(googleToken);
          localStorage.setItem("access_token", response.data.access_token)
          this.$emit("emitChangeLogin", true);
          // this.taskData = response.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    onFailure (googleUser) {
      console.log(googleUser)
    },
  },
};
</script>

<style scoped>
.googlebutton {
  display: flex;
  justify-content: center;
}
</style>