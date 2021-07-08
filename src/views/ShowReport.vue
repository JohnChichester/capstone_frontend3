<template>
  <div class="ShowReport">
    <!--{{ report }}-->
    <p>Any misc tracking was due to...</p>
    <div>{{ report.misc }}</div>
    <p>Hours Worked</p>
    <div>{{ report.worked }}</div>
    <p>Square ft. Printed</p>
    <div>{{ report.printed }}</div>
    <p>Square ft. Cut</p>
    <div>{{ report.cut }}</div>

    <div class="card">
      <div class="card-header">
        <h3 class="card-title">EOD Report: {{ report.Date }}</h3>
      </div>
      <!-- /.card-header -->
      <div class="card-body">
        <!-- we are adding the accordion ID so Bootstrap's collapse plugin detects it -->
        <div id="accordion">
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseOne">Safety</a>
              </h4>
            </div>
            <div id="collapseOne" class="collapse show" data-parent="#accordion">
              <div class="card-body">
                {{ report.safety }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseTwo">Sustain</a>
              </h4>
            </div>
            <div id="collapseTwo" class="collapse" data-parent="#accordion">
              <div class="card-body">
                {{ report.sustain }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseThree">Shine</a>
              </h4>
            </div>
            <div id="collapseThree" class="collapse" data-parent="#accordion">
              <div class="card-body">
                {{ report.shine }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseThree">Sort</a>
              </h4>
            </div>
            <div id="collapseFour" class="collapse" data-parent="#accordion">
              <div class="card-body">
                {{ report.sort }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseThree">Set In Order</a>
              </h4>
            </div>
            <div id="collapseFive" class="collapse" data-parent="#accordion">
              <div class="card-body">
                {{ report.set_in_order }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseThree">Standardize</a>
              </h4>
            </div>
            <div id="collapseSix" class="collapse" data-parent="#accordion">
              <div class="card-body">
                {{ report.standardize }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseThree">Misc</a>
              </h4>
            </div>
            <div id="collapseSeven" class="collapse" data-parent="#accordion">
              <div class="card-body">
                {{ report.misc }}
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- /.card-body -->
    </div>
    <!-- /.card -->
  </div>
</template>

<script>
//../../plugins/jquery/jquery.min.js">
//<!-- Bootstrap 4 -->
//"../../plugins/bootstrap/js/bootstrap.bundle.min.js">
//<!-- AdminLTE App -->
//"../../dist/js/adminlte.min.js">

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
