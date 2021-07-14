<template>
  <div class="Login">
    <div class="card card-primary">
      <div class="card-header">
        <h3 class="card-title">Login</h3>
      </div>
      <!-- /.card-header -->
      <!-- form start -->
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <form v-on:submit.prevent="submit()">
        <div class="card-body">
          <div class="form-group">
            <label for="username">Username</label>
            <input type="username" v-model="username" class="form-control" placeholder="Enter Username" />
          </div>
          <div class="form-group">
            <label for="password1">Password</label>
            <input type="password" v-model="password" class="form-control" placeholder="Password" />
          </div>
        </div>
        <!-- /.card-body -->

        <div class="card-footer">
          <button type="submit" class="btn btn-primary">Submit</button>
        </div>
      </form>
    </div>
    <!-- /.card -->
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      username: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submit: function () {
      var params = {
        username: this.username,
        password: this.password,
      };
      axios
        .post("/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          localStorage.setItem("admin", response.data.admin);
          this.$router.push("/");
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid username or password."];
          this.username = "";
          this.password = "";
        });
    },
  },
};
</script>
