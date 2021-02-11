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
          <form class="d-flex">
            <button class="btn btn-outline-success" type="submit">
              Logout
            </button>
          </form>
        </div>
      </div>
    </nav>
    <br /><br />

    <!-- CARD -->
    <section class="d-flex justify-content-around">
      <!-- BACKLOG -->
      <div class="bg-info text-white rounded">
        <h4 class="m-2 text-center">Backlog</h4>

        <div class="m-3 card text-dark">
          <div class="card-header">Title</div>
          <div class="card-body">
            <h5 class="card-title">title</h5>
            <p class="card-text">text content</p>
            <div class="d-flex justify-content-end">
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-primary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#editModal"
                >Edit</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-secondary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#moveModal"
                >Move</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-danger rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#deleteModal"
                >Delete</a
              >
            </div>
          </div>
        </div>

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

      <!-- TODO -->
      <div class="bg-info text-white rounded">
        <h4 class="m-2 text-center">Todo</h4>

        <div class="m-3 card text-dark">
          <div class="card-header">Title</div>
          <div class="card-body">
            <h5 class="card-title">title</h5>
            <p class="card-text">text content</p>
            <div class="d-flex justify-content-end">
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-primary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#editModal"
                >Edit</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-secondary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#moveModal"
                >Move</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-danger rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#deleteModal"
                >Delete</a
              >
            </div>
          </div>
        </div>

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

      <!-- DOING -->
      <div class="bg-info text-white rounded">
        <h4 class="m-2 text-center">Doing</h4>
        <div class="m-3 card text-dark">
          <div class="card-header">Title</div>
          <div class="card-body">
            <h5 class="card-title">title</h5>
            <p class="card-text">text content</p>
            <div class="d-flex justify-content-end">
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-primary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#editModal"
                >Edit</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-secondary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#moveModal"
                >Move</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-danger rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#deleteModal"
                >Delete</a
              >
            </div>
          </div>
        </div>
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

      <!-- COMPLETE -->
      <div class="bg-info text-white rounded">
        <h4 class="m-2 text-center">Complete</h4>
        <div class="m-3 card text-dark">
          <div class="card-header">Title</div>
          <div class="card-body">
            <h5 class="card-title">title</h5>
            <p class="card-text">text content</p>
            <div class="d-flex justify-content-end">
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-primary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#editModal"
                >Edit</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-secondary rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#moveModal"
                >Move</a
              >
              <a
                href="#"
                class="m-2 btn btn-sm btn-outline-danger rounded-pill"
                data-bs-toggle="modal"
                data-bs-target="#deleteModal"
                >Delete</a
              >
            </div>
          </div>
        </div>
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
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  methods: {
    getTasks() {
      axios({
        method: "GET",
        url: "http://localhost:3000/tasks",
        headers: {
          access_token: localStorage.access_token,
        },
      })
        .then(({ data }) => {
          console.log(data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  created() {
    this.getTasks();
  },
};
</script>

<style>
</style>