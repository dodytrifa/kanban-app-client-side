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
  <!-- <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Modal title</h5>
              <button
                type="button"
                class="close"
                data-dismiss="modal"
                aria-label="Close"
              >
                <span aria-hidden="true" @click="showModal">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <p>Modal body text goes here.</p>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary">Close</button>
              <button type="button" class="btn btn-primary">
                Save changes
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition> -->
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
    showModal() {
      this.$emit("showModal", false);
    },
  },
};
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
</style>