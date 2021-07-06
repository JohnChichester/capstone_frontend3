<template>
  <div id="app">
    <aside class="main-sidebar sidebar-dark-primary elevation-4">
      <nav class="mt-2">
        <ul class="nav nav-pills nav-sidebar flex-column" data-widget="treeview" role="menu" data-accordion="false">
          <li class="nav-item">
            <a href="/" class="nav-link">
              <i class="nav-icon fas fa-house-user"></i>
              <p>Home</p>
            </a>
          </li>
          <li class="nav-item">
            <a href="/about" class="nav-link">
              <i class="nav-icon fas fa-chalkboard"></i>
              <p>About</p>
            </a>
          </li>

          <li v-if="isLoggedIn()" class="nav-item">
            <a href="/CreateReport" class="nav-link">
              <i class="nav-icon fas fa-clipboard-list"></i>
              <p>Create Report</p>
            </a>
          </li>
          <li v-if="!isLoggedIn()" class="nav-item">
            <a href="/signup" class="nav-link">
              <i class="nav-icon fas fa-user"></i>
              <p>Signup</p>
            </a>
          </li>

          <li v-if="!isLoggedIn()" class="nav-item">
            <a href="/login" class="nav-link">
              <i class="nav-icon fas fa-lock-open"></i>
              <p>Login</p>
            </a>
          </li>

          <li v-if="isLoggedIn()" class="nav-item">
            <a href="/logout" class="nav-link">
              <i class="nav-icon fas fa-door-open"></i>
              <p>Logout</p>
            </a>
          </li>
        </ul>
      </nav>
    </aside>
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
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
