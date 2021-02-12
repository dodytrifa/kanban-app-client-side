<template>
  <div>
    <Kanban
      v-if="isLogin"
      @getTasks="getTasks"
      :taskData="taskData"
      @destroyTask="destroyTask"
      @editTask="editTask"
    ></Kanban>
    <Login
      v-if="!isLogin"
      :dataIsLogin="isLogin"
      @emitChangeLogin="changeIsLogin"
      :urlServer="urlServer"
    ></Login>
    <!-- <Register v-if="isLogin" :urlServer="urlServer"></Register> -->
  </div>
</template>

<script>
import Login from "./views/Login";
import Register from "./views/Register";
import Kanban from "./views/Kanban";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      isLogin: false,
      page: "",
      urlServer: "http://localhost:3000",
      taskData: [],
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
    directPage(page) {
      this.page = page;
    },
    getTasks() {
      axios({
        method: "GET",
        // url: "http://localhost:3000/tasks",
        url: `${this.urlServer}/tasks`,
        headers: {
          access_token: localStorage.access_token,
        },
      })
        .then((response) => {
          // console.log(response.data);
          this.taskData = response.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    destroyTask(id) {
      axios({
        url: `${this.urlServer}/tasks/` + id,
        method: "DELETE",
        headers: {
          access_token: localStorage.getItem("access_token"),
        },
      })
        .then((response) => {
          this.getTasks();
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    editTask(id) {
      // console.log("dari App");
      axios({
        url: `${this.urlServer}/tasks/` + id,
        method: "PUT",
        headers: {
          access_token: localStorage.getItem("access_token"),
        },
      })
        .then((response) => {
          // this.getTasks();
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    addTask() {
      // console.log("dari App");
      axios({
        url: `${this.urlServer}/tasks/`,
        method: "POST",
        headers: {
          access_token: localStorage.getItem("access_token"),
        },
      })
        .then((response) => {
          // this.getTasks();
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
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