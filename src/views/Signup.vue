<template>
  <div class="Signup">
    <div class="card card-primary">
      <div class="card-header">
        <h3 class="card-title">Create User</h3>
      </div>
      <!-- /.card-header -->
      <!-- form start -->
      <form v-on:submit.prevent="submit()">
        <div class="card-body">
          <div></div>
          <div class="form-group">
            <label for="first_name">First Name:</label>
            <input type="first_name" class="form-control" v-model="first_name" placeholder="Enter name" />
          </div>
          <div class="form-group">
            <label for="last_name">Last Name:</label>
            <input type="last_name" class="form-control" v-model="last_name" placeholder="Enter name" />
          </div>
          <div class="form-group">
            <label for="department">Department:</label>
            <select class="form-control" v-model="department">
              <option>Production</option>
              <option>Pre-press</option>
              <option>Marketing</option>
              <option>Sales</option>
              <option>Management</option>
            </select>
          </div>
          <div class="form-group">
            <label for="last_name">Password:</label>
            <input
              type="password"
              class="form-control"
              v-model="password"
              placeholder="Passwords must contain 3 prime numbers and the symbol of a forgotten god"
            />
          </div>
          <div class="form-group">
            <label for="last_name">Password confirmation</label>
            <input type="password" class="form-control" v-model="passwordConfirmation" />
          </div>
        </div>
        <!-- /.card-body -->

        <div class="card-footer">
          <button type="submit" class="btn btn-primary">Submit</button>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
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
      first_name: "",
      last_name: "",
      username: "",
      department: "",
      password: "",
      passwordConfirmation: "",
      errors: [],
    };
  },
  methods: {
    submit: function () {
      var params = {
        first_name: this.first_name,
        last_name: this.last_name,
        username: this.first_name[0].toUpperCase() + this.last_name.toLowerCase(),
        department: this.department,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post("/users", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
