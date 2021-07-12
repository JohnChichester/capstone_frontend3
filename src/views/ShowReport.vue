<template>
  <div class="ShowReport">
    <!--{{ report }}-->
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
                <h5>Are there any safety concerns?</h5>
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
                <h5>Did you leave your workspace in better condition than when you arrived?</h5>
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
                <h5>
                  Report of Quality Issues, Concerns for Review (All materials have nice clean edges and are neatly
                  stacked on pallets):
                </h5>
                {{ report.shine }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseFour">Sort</a>
              </h4>
            </div>
            <div id="collapseFour" class="collapse" data-parent="#accordion">
              <div class="card-body">
                <h5>Was your schedule completed and work tracked accurately?</h5>
                {{ report.sort }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseFive">Set In Order</a>
              </h4>
            </div>
            <div id="collapseFive" class="collapse" data-parent="#accordion">
              <div class="card-body">
                <h5>Was the needed material tagged properly for production?</h5>
                {{ report.set_in_order }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseSix">Standardize</a>
              </h4>
            </div>
            <div id="collapseSix" class="collapse" data-parent="#accordion">
              <div class="card-body">
                <h5>
                  Did you receive job bags that were properly signed and contained all needed items for production?
                </h5>
                {{ report.standardize }}
              </div>
            </div>
          </div>
          <div class="card card-secondary">
            <div class="card-header">
              <h4 class="card-title w-100">
                <a class="d-block w-100" data-toggle="collapse" href="#collapseSeven">Misc</a>
              </h4>
            </div>
            <div id="collapseSeven" class="collapse" data-parent="#accordion">
              <div class="card-body">
                <h5>Any misc tracking was due to...</h5>
                {{ report.misc }}
                <div class="row">
                  <div class="col-md-3 col-sm-6 col-12">
                    <div class="info-box">
                      <span class="info-box-icon bg-info"><i class="far fa-clock"></i></span>

                      <div class="info-box-content">
                        <span class="info-box-number">Hours</span>
                        <span class="info-box-number">{{ report.worked }}</span>
                      </div>
                      <!-- /.info-box-content -->
                    </div>
                    <!-- /.info-box -->
                  </div>
                  <div class="col-md-3 col-sm-6 col-12">
                    <div class="info-box">
                      <span class="info-box-icon bg-info"><i class="fa-solid fa-print"></i></span>

                      <div class="info-box-content">
                        <span class="info-box-number">Square ft. Printed</span>
                        <span class="info-box-number">{{ report.printed }}</span>
                      </div>
                      <!-- /.info-box-content -->
                    </div>
                    <!-- /.info-box -->
                  </div>
                  <div class="col-md-3 col-sm-6 col-12">
                    <div class="info-box">
                      <span class="info-box-icon bg-info"><i class="fa-solid fa-hand-scissors"></i></span>

                      <div class="info-box-content">
                        <span class="info-box-number">Square ft. Cut</span>
                        <span class="info-box-number">{{ report.cut }}</span>
                      </div>
                      <!-- /.info-box-content -->
                    </div>
                    <!-- /.info-box -->
                  </div>
                </div>
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
