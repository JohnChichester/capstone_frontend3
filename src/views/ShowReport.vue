<template>
  <div class="ShowReport">
    <!--{{ report }}-->
    <h1>EOD Report: {{ report.Date }}</h1>
    <h4>Safety</h4>
    <div>{{ report.safety }}</div>
    <h4>Sustain</h4>
    <div>{{ report.sustain }}</div>
    <h4>Shine</h4>
    <div>{{ report.shine }}</div>
    <h4>Sort</h4>
    <div>{{ report.sort }}</div>
    <h4>Set In Order</h4>
    <div>{{ report.set_in_order }}</div>
    <h4>Standardize</h4>
    <div>{{ report.standardize }}</div>
    <p>Anyisc tracking was due to...</p>
    <div>{{ report.misc }}</div>
    <p>Hours Worked</p>
    <div>{{ report.worked }}</div>
    <p>Square ft. Printed</p>
    <div>{{ report.printed }}</div>
    <p>Square ft. Cut</p>
    <div>{{ report.cut }}</div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      report: {},
      current_user: "",
      status: null,
    };
  },
  created: function () {
    axios.get("/reports/" + this.$route.params.id).then((response) => {
      console.log("report show", response);
      this.report = response.data;
    });
  },
  methods: {},
};
//updateReport: function (post) {
// var params = {
// title: report.id,
// };
// axios.patch("/reports/" + report.id, params).then((response) => {
//  report.safety: "",
//  report.sustain: "",
//  report.shine: "",
//  report.sort: "",
//  report.set_in_order: "",
//  report.standardize: "",
//  report.misc: "",
//  report.worked: 8,
//  report.printed: "",
//  report.cut: "",
//  errors: [],
//  this.currentReport = {};
// })
// .catch((error) => {
//   console.log(error.response);
// });
</script>
