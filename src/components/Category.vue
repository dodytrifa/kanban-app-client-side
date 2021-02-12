<template>
  <div class="m-3 bg-info card text-white d-flex justify-content-center">
    <div class="card-header">
      <h4 class="m-2 text-center">{{ eachCategory }}</h4>
    </div>
    <div class="card-body">
      <Task
        v-for="task in findTaskByCategory"
        :key="task.id"
        :categoryContainer="task"
        @destroyTask="destroyTask"
        @editTask="editTask"
      ></Task>

      <div class="d-flex justify-content-end">
        <div class="p-3 d-flex justify-content-end">
          <a
            href="#"
            class="btn btn-sm btn-primary rounded-pill"
            data-bs-toggle="modal"
            data-bs-target="#addModal"
            >Add</a
          >
        </div>
      </div>
    </div>

    <!--tes CARD  -->

    <!-- tes CARD -->
  </div>
</template>

<script>
import Task from "../components/Task";
export default {
  name: "Category",
  components: {
    Task,
  },
  props: ["eachCategory", "taskData"],
  methods: {
    destroyTask(id) {
      // console.log("dari category");
      this.$emit("destroyTask", id);
    },
    editTask(id) {
      // console.log("dari category");
      this.$emit("editTask", id);
    },
    addTask() {
      // console.log("dari category");
      this.$emit("addTask");
    },
  },
  computed: {
    findTaskByCategory() {
      let categoryContainer = [];
      for (let i = 0; i < this.taskData.length; i++) {
        if (this.taskData[i].category === this.eachCategory) {
          categoryContainer.push(this.taskData[i]);
        }
      }
      return categoryContainer;
    },
  },
};
</script>

<style>
</style>