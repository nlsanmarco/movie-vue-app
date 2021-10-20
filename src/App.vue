<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <router-link class="navbar-brand" to="/">Movies</router-link>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li v-if="isLoggedIn()" class="nav-item">
              <router-link class="nav-link active" aria-current="page" to="/logout">Logout</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/signup">Signup</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/login">Login</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies">Movies</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies/new">New Movie</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/actors">Actors</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/actors/new">New Actor</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
<script>
export default {
  data: function () {
    return {};
  },
  created: function () {},
  methods: {
    isLoggedIn() {
      return localStorage.jwt;
    },
  },
};
</script>
