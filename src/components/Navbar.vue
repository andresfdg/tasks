<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <div class="container-fluid">
      <a class="navbar-brand" href="#"><h1>Tasks</h1></a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarTogglerDemo02"
        aria-controls="navbarTogglerDemo02"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarTogglerDemo02">
        <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link to="/" class="nav-link">Log In</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/about" class="nav-link">Register</router-link>
          </li>
          <li>
            <router-link to="/projects" class="nav-item btn btn-danger"
              >Projects</router-link
            >
          </li>
          <li>
            <router-link
              to="/"
              class="nav-item btn btn-danger"
              @click.prevent="close"
              >Log Out</router-link
            >
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  methods: {
    close() {
      localStorage.removeItem("user");
    },
  },
};
</script>

<style scoped></style>
