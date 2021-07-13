<template>
  <div id="app">
    <div class="wrapper">
      <!-- Navbar -->
      <nav class="main-header navbar navbar-expand navbar-dark"></nav>
      <!-- /.navbar -->

      <!-- Main Sidebar Container -->
      <div class="card card-secondary">
        <div class="card-header" />
      </div>
      <aside class="main-sidebar sidebar-dark-primary elevation-4">
        <a href="/" class="brand-link">
          <span class="brand-text font-weight-light">SCRAMGILE</span>
        </a>
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
            <!--<li class="nav-item menu-open">
              <a href="#" class="nav-link active">
                <i class="fa-calculator"></i>
                <p>
                  Calculator
                  <i class="right fas fa-angle-left"></i>
                </p>
              </a>
              <ul class="nav nav-treeview">
                <div>
                  <calculator />
                </div>
              </ul>
            </li>-->
          </ul>
        </nav>
      </aside>

      <!-- Content Wrapper. Contains page content -->
      <div class="content-wrapper">
        <!-- Content Header (Page header) -->
        <div class="content-header">
          <div class="container-fluid">
            <div class="row mb-2">
              <div class="col-sm-6">
                <h1 class="m-0"></h1>
              </div>
              <!-- /.col -->
              <div class="col-sm-6">
                <ol class="breadcrumb float-sm-right"></ol>
              </div>
              <!-- /.col -->
            </div>
            <!-- /.row -->
          </div>
          <!-- /.container-fluid -->
        </div>
        <!-- /.content-header -->

        <!-- Main content -->
        <section class="content">
          <div class="container-fluid">
            <router-view />
          </div>
          <!--/. container-fluid -->
        </section>
        <!-- /.content -->
      </div>
      <!-- /.content-wrapper -->

      <!-- Control Sidebar -->
      <aside class="control-sidebar control-sidebar-dark">
        <!-- Control sidebar content goes here -->
      </aside>
      <!-- /.control-sidebar -->
    </div>
  </div>
</template>

<style></style>

<script>
//import Calculator from "@/components/Calculator.vue";

export default {
  components: {
    // Calculator,
  },
  data: function () {
    return {
      admin: false,
      currentUser: {},
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    isAdmin: function () {
      return localStorage.getItem("admin");
    },
  },
};
</script>
