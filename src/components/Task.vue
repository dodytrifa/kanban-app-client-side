<template>
  <div class="m-3 card text-dark">
    <div class="card-header">
      <h5 class="m-2 text-center">{{ categoryContainer.title }}</h5>
    </div>
    <div class="card-body">
      <p class="card-text">{{ categoryContainer.title }}</p>
      <div class="d-flex justify-content-end">
        <button
          @click.prevent="directPage"
          type="button"
          class="m-2 btn btn-sm btn-outline-primary rounded-pill"
        >
          Edit/ Move
        </button>

        <button
          type="button"
          class="m-2 btn btn-sm btn-outline-danger rounded-pill"
          @click="destroyTask"
        >
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: ["categoryContainer"],
  methods: {
    directPage(value) {
      this.$emit("emitDirectPage", "EditTask", this.categoryContainer.id);
      localStorage.setItem(
        "selectedTask",
        JSON.stringify(this.categoryContainer)
      );
    },
    destroyTask() {
      this.$emit("destroyTask", this.categoryContainer.id);
    },
    editTask() {
      this.$emit("editTask", this.categoryContainer.id);
    },
  },
};
</script>

<style>
</style>