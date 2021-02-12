<template>
  <div class="m-3 card text-dark">
    <div class="card-header">
      <h5 class="m-2 text-center">{{ categoryContainer.title }}</h5>
    </div>
    <div class="card-body">
      <p class="card-text">{{ categoryContainer.title }}</p>
      <div class="d-flex justify-content-end">
        <button
          type="button"
          class="m-2 btn btn-sm btn-outline-primary rounded-pill"
          @click="editTask"
        >
          Edit
        </button>
        <a
          type="button"
          class="m-2 btn btn-sm btn-outline-secondary rounded-pill"
          >Move</a
        >
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