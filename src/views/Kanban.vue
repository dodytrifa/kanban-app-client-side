<template>
  <div>
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid">
        <h1 class="navbar-brand">Kanban App</h1>

        <button
          @click.prevent="logout"
          class="btn btn-outline-danger"
          type="submit"
        >
          Logout
        </button>
      </div>
    </nav>
    <br />
    <p align="center" style="color: red" v-if="authorizationCheck">
      {{ authorization }}
    </p>
    <div class="container-fluid d-flex justify-content-around">
      <div class="row">
        <Category
          v-for="(category, index) in categories"
          :key="index"
          :taskData="taskData"
          :authorization="authorizationCheck"
          :eachCategory="category"
          @destroyTask="destroyTask"
          @editTask="editTask"
          @emitDirectPage="directPage"
        ></Category>
      </div>
    </div>
  </div>
</template>

<script>
import Category from "../components/Category.vue";
import Task from "../components/Task.vue";
export default {
  data() {
    return {
      categories: ["Backlog", "Todo", "Doing", "Complete"],
      page: "kanban",
    };
  },
  components: {
    Category,
    Task,
  },
  props: ["taskData", "authorizationCheck"],
  methods: {
    destroyTask(id) {
      this.$emit("destroyTask", id);
    },
    editTask(id) {
      this.$emit("editTask", id);
    },
    addTask() {
      console.log("dari kanban");
    },
    directPage(value) {
      this.$emit("emitDirectPage", value);
    },
    logout() {
      this.$emit("logout");
    },
  },
  created() {
    this.$emit("getTasks");
  },
};
</script>

<style>
</style>