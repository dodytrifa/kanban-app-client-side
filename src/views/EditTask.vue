<template>
  <div class="d-flex justify-content-center">
    <form @submit.prevent="editTask" id="edit-form">
      <h3>Edit Existing Task</h3>
      <br />
      <div class="mb-3">
        <label for="input-task" class="form-label">Edit Task Category</label>
        <select
          v-model="selected"
          class="form-select"
          aria-label="Default select example"
        >
          <option disabled value>Choose the task category</option>
          <option value="Backlog">Backlog</option>
          <option value="Todo">Todo</option>
          <option value="Doing">Doing</option>
          <option value="Complete">Complete</option>
        </select>
      </div>

      <div class="mb-3">
        <label for="edit-input" class="form-label">Edit Task</label>
        <input v-model="titleInput" type="text" class="form-control-login" />
      </div>
      <button type="submit" class="btn btn-primary">Submit</button><br /><br />
    </form>
  </div>
</template>

<script>

export default {
  name: "EditTask",
  props: ["urlServer", "id"],
  data() {
    return {
      page: "EditTask",
      selected: "",
      titleInput: "",
    };
  },
  methods: {
    editTask() {
      this.$emit("editTask", this.selected, this.titleInput);
    },
  },
};
</script>

<style>
</style>