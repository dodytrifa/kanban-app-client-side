<template>
  <div>
    <Kanban
      v-if="isLogin"
      :taskData="taskData"
      :authorization="authorizationCheck"
      @getTasks="getTasks"
      @destroyTask="destroyTask"
      @editTask="editTask"
      @emitDirectPage="directPage"
      @logout="logout"
    ></Kanban>
    <Login
      v-if="!isLogin && page === 'login'"
      :dataIsLogin="isLogin"
      :urlServer="urlServer"
      @emitChangeLogin="changeIsLogin"
      @emitDirectPage="directPage"
    ></Login>
    <Register
      v-if="page === 'register'"
      :urlServer="urlServer"
      @emitDirectPage="directPage"
    ></Register>
    <AddTask
      v-if="page === 'AddTask'"
      :urlServer="urlServer"
      @addTask="addTask"
      @getTasks="getTasks"
      @emitDirectPage="directPage"
    ></AddTask>
    <EditTask
      v-if="page === 'EditTask'"
      :urlServer="urlServer"
      @editTask="editTask"
      @getTasks="getTasks"
      :id="selectedTask"
    ></EditTask>
  </div>
</template>

<script>
import Login from "./views/Login";
import Register from "./views/Register";
import Kanban from "./views/Kanban";
import AddTask from "./views/AddTask";
import EditTask from "./views/EditTask";

import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      isLogin: false,
      page: "login",
      urlServer: "https://kanban-app-dody.herokuapp.com",
      // urlServer: "http://localhost:3000",
      taskData: [],
      selectedTask: "",
      authorizationCheck: "",
    };
  },
  components: {
    Login,
    Register,
    Kanban,
    AddTask,
    EditTask,
  },
  methods: {
    changeIsLogin(value) {
      this.isLogin = value;
    },
    directPage(value, id) {
      this.page = value;
      this.selectedTask = id;
    },

    getTasks() {
      axios({
        method: "GET",
        url: `${this.urlServer}/tasks`,
        headers: {
          access_token: localStorage.access_token,
        },
      })
        .then((response) => {
          this.taskData = response.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    addTask(selected, taskInput) {
      axios({
        method: "POST",
        url: `${this.urlServer}/tasks/`,
        headers: {
          access_token: localStorage.getItem("access_token"),
        },
        data: {
          category: selected,
          title: taskInput,
        },
      })
        .then((response) => {
          this.getTasks();
          this.page = "login";
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
          this.page = "login";
          console.log(response.data.message);
        })
        .catch((err) => {
          console.log(err.response.data.message);
        });
    },
    editTask(selected, titleInput) {
      const dataTask = JSON.parse(localStorage.getItem("selectedTask"));
      axios({
        url: `${this.urlServer}/tasks/` + dataTask.id,
        method: "PUT",
        headers: {
          access_token: localStorage.getItem("access_token"),
        },
        data: {
          category: selected,
          title: titleInput,
        },
      })
        .then((response) => {
          this.getTasks();
          this.page = "login";
        })
        .catch((err) => {
          console.log(err.response.data.message);
          this.authorizationCheck = err.response.data.message;
        });
    },

    logout() {
      localStorage.clear();
      this.isLogin = false;
      this.page = "login";
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