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
import axios from "axios";

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
      // console.log(this.id);
      // const dataTask = JSON.parse(localStorage.getItem("selectedTask"));
      // axios({
      //   url: `${this.urlServer}/tasks/` + dataTask.id,
      //   method: "PUT",
      //   headers: {
      //     access_token: localStorage.getItem("access_token"),
      //   },
      //   data: {
      //     category: this.selected,
      //     title: this.titleInput,
      //   },
      // })
      //   .then((response) => {
      //     console.log(this.selected);
      //     console.log(this.titleInput);
      //     console.log(this.id);
      //     console.log(response);
      //   })
      //   .catch((err) => {
      //     console.log(err);
      //   });
    },
  },
};
</script>

<style>
</style>