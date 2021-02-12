<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light text-white bg-info">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Kanban App</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0"></ul>
          <form class="d-flex flex-end">
            <button
              class="d-flex flex-end btn btn-outline-bg-info"
              type="submit"
            >
              Logout
            </button>
          </form>
        </div>
      </div>
    </nav>
    <br /><br />

    <div class="container-fluid d-flex justify-content-around">
      <div class="row">
        <Category
          v-for="(category, index) in categories"
          :key="index"
          :taskData="taskData"
          :eachCategory="category"
          @destroyTask="destroyTask"
          @editTask="editTask"
          @addTask="addTask"
        ></Category>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios";
import Category from "../components/Category.vue";
import Task from "../components/Task.vue";
export default {
  data() {
    return {
      categories: ["Backlog", "Todo", "Doing", "Complete"],
    };
  },
  components: {
    Category,
    Task,
  },
  props: ["taskData"],
  methods: {
    destroyTask(id) {
      // console.log("del dari kanban");
      this.$emit("destroyTask", id);
    },
    editTask(id) {
      // console.log("dari kanban");
      this.$emit("editTask", id);
    },
    addTask() {},
  },
  // methods: {
  //   getTasks() {
  //     axios({
  //       method: "GET",
  //       url: "http://localhost:3000/tasks",
  //       headers: {
  //         access_token: localStorage.access_token,
  //       },
  //     })
  //       .then(({ data }) => {
  //         console.log(data);
  //       })
  //       .catch((err) => {
  //         console.log(err);
  //       });
  //   },
  // },
  created() {
    this.$emit("getTasks");
  },
};
</script>

<style>
</style>