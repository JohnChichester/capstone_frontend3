<template>
  <div class="Report">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>First Name:</label>
        <input type="text" v-model="first_name" />
      </div>

      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
