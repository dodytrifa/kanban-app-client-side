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
        @emitDirectPage="directPage"
      ></Task>

      <div class="d-flex justify-content-end">
        <div class="p-3 d-flex justify-content-end">
          <button
            @click.prevent="directPage"
            type="button"
            class="btn btn-sm btn-primary rounded-pill"
          >
            Add
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Task from "../components/Task";
export default {
  name: "Category",
  data() {
    return {
      dataTask: [],
    };
  },
  components: {
    Task,
  },
  props: ["eachCategory", "taskData"],
  methods: {
    directPage(value) {
      if (value === "EditTask") {
        this.$emit("emitDirectPage", "EditTask");
      } else {
        this.$emit("emitDirectPage", "AddTask");
      }
    },
    destroyTask(id) {
      this.$emit("destroyTask", id);
    },
    editTask(id) {
      this.$emit("editTask", id);
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
  // created(){
  //   let categoryContainer = [];
  //     for (let i = 0; i < this.taskData.length; i++) {
  //       if (this.taskData[i].category === this.eachCategory) {
  //         categoryContainer.push(this.taskData[i]);
  //       }
  //     }
  //     this.dataTask = categoryContainer
  // }
};
</script>

<style>
</style>