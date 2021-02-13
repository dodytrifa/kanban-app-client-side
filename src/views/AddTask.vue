<template>
  <div class="d-flex justify-content-center">
    <form @submit.prevent="addTask" id="add-form">
      <h3>Add new task</h3>
      <br />
      <div class="mb-3">
        <label for="input-task" class="form-label">New Task Category</label>
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
        <label for="input-task" class="form-label">New Task</label>
        <input v-model="taskInput" type="text" class="form-control-login" />
      </div>
      <button type="submit" class="btn btn-primary">Submit</button><br /><br />
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTask",
  props: ["urlServer"],
  data() {
    return {
      page: "AddTask",
      selected: "",
      taskInput: "",
    };
  },
  methods: {
    addTask() {
      this.$emit("addTask", this.selected, this.taskInput);
    },
  },
};
</script>

<style>
</style>