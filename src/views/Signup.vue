<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>First Name:</label>
        <input type="text" v-model="first_name" />
      </div>
      <div>
        <label>Last Name:</label>
        <input type="text" v-model="last_name" />
      </div>
      <div>
        <label>Department:</label>
        <input type="text" v-model="department" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="password" />
      </div>
      <div>
        <label>Password Confirmation:</label>
        <input type="password" v-model="passwordConfirmation" />
      </div>
      <input type="submit" value="Submit" />
    </form>
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
