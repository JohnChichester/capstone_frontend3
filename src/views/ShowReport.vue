<template>
  <div class="ShowReport"></div>
</template>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      reports: [],
      current_user: "",
      status: null,
    };
  },
  created: function () {
    this.showReport();
  },
  methods: {
    showReport: function () {
      axios.get("/reports/:id").find_bythen((response) => {
        this.reports = response.data;
        console.log(this.reports);
      });
    },
  },
};
</script>
