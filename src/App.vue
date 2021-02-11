<template>
  <div>
    <Kanban v-if="isLogin"></Kanban>
    <Login
      v-if="!isLogin"
      :dataIsLogin="isLogin"
      @emitChangeLogin="changeIsLogin"
      :urlServer="urlServer"
    ></Login>
    <!-- <Register></Register> -->
  </div>
</template>

<script>
import Login from "./views/Login";
import Register from "./views/Register";
import Kanban from "./views/Kanban";

export default {
  data() {
    return {
      isLogin: false,
      page: "",
      urlServer: "http://localhost:3000",
    };
  },
  components: {
    Login,
    Register,
    Kanban,
  },
  methods: {
    changeIsLogin(value) {
      this.isLogin = value;
    },
  },
  created() {
    if (localStorage.access_token) {
      this.isLogin = true;
    } else {
      this.isLogin = false;
    }
  },
};
</script>

<style>
</style>