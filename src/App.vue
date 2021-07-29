<template>
  <div id="app">
    <div id="nav">
      <li>
        <router-link to="/">Home</router-link>
      </li>
      |
      <li>
        <router-link to="/about">About</router-link>
      </li>
      |
      <li>
        <router-link to="/test">Test</router-link>
      </li>
      |
      <li v-if="!isLoggedIn()">
        <router-link to="/signup">Signup</router-link>
      </li>
      |
      <li v-if="!isLoggedIn()">
        <router-link to="/login">Login</router-link>
      </li>
      |
      <li v-if="isLoggedIn()">
        <router-link to="/logout">Logout</router-link>
      </li>
      |
      <li>
        <router-link to="/posts">Posts</router-link>
      </li>
      |
      <li>
        <router-link to="/posts/new">Create</router-link>
      </li>
    </div>
    <!-- <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="/">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/signup">Signup</a>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              Dropdown
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="#">Action</a>
              <a class="dropdown-item" href="#">Another action</a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav> -->
    <router-view />
  </div>
</template>

<style>
body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: rgb(239, 226, 247) !important;
  background-image: url("./assets/baroque-pattern.jpeg");
  text-align: center;
}
</style>

<script>
// import axios from "axios";
export default {
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
