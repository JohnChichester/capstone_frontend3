<template>
  <div class="Home">
    <div class="card card-primary">
      <div class="card-header">
        <h3 class="card-title">Workplace Moral</h3>

        <div class="card-tools">
          <button type="button" class="btn btn-tool" data-card-widget="collapse">
            <i class="fas fa-minus"></i>
          </button>
          <button type="button" class="btn btn-tool" data-card-widget="remove">
            <i class="fas fa-times"></i>
          </button>
        </div>
      </div>
      <div class="card-body">
        <div>
          <apexchart height="310" type="area" :options="chartOptions" :series="series"></apexchart>
        </div>
      </div>
      <!-- /.card-body -->
    </div>
    <!-- /.card -->

    <div class="card-body">
      <ul class="pagination pagination-month justify-content-center">
        <li class="page-item"><a class="page-link" href="#">«</a></li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Jan</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item active">
          <a class="page-link" href="#">
            <p class="page-month">Feb</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Mar</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Apr</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">May</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Jun</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Jul</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Aug</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Sep</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Oct</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Nov</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">
            <p class="page-month">Dec</p>
            <p class="page-year">2021</p>
          </a>
        </li>
        <li class="page-item"><a class="page-link" href="#">»</a></li>
      </ul>
    </div>

    <div class="row justify-content-center">
      <div class="card">
        <div class="card-header border-transparent">
          <h3 class="card-title">
            <p v-if="isAdmin()">All Reports</p>
            <p v-if="!isAdmin()">My Reports</p>
          </h3>
        </div>
        <!-- /.card-header -->
        <div class="card-body p-0">
          <div class="table-responsive">
            <table class="table m-0">
              <thead>
                <tr>
                  <th>=)</th>
                  <th>Date</th>
                  <th>Hours</th>
                  <th>Tagged Jobs</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="report in reports" v-bind:key="report.id">
                  <td>{{ report.good_day_bad_day }}</td>
                  <td>
                    <router-link v-bind:to="`/reports/${report.id}`">{{ report.Date }}</router-link>
                  </td>
                  <td>
                    <span class="badge badge-success">{{ report.worked }}</span>
                  </td>
                  <td>
                    <div class="sparkbar" data-color="#00a65a" data-height="20">{{ report.tagged_jobs }}</div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
          <!-- /.table-responsive -->
        </div>
        <!-- /.card-body -->
      </div>
      <!-- /.card -->
      <div class="card">
        <div class="card-header border-transparent">
          <h3 class="card-title">
            <p>Production Totals</p>
          </h3>
        </div>
        <!-- /.card-header -->
        <div class="card-body p-0">
          <div class="table-responsive">
            <table class="table m-0">
              <thead>
                <tr>
                  <th>Summary Totals</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>4300</td>
                  <td>Sq Ft Printed</td>
                </tr>
                <tr>
                  <td>3300</td>
                  <td>Sq Ft Cut</td>
                </tr>
                <tr>
                  <td>720</td>
                  <td>Total Hours</td>
                </tr>
                <tr>
                  <td>120</td>
                  <td>Overtime</td>
                </tr>
              </tbody>
            </table>
          </div>
          <!-- /.table-responsive -->
        </div>
        <!-- /.card-body -->
      </div>
      <!-- /.card -->
    </div>
  </div>
</template>

<script>
import axios from "axios";
import VueApexCharts from "vue-apexcharts";

export default {
  components: {
    apexchart: VueApexCharts,
  },

  data: function () {
    return {
      reports: [],
      current_user: {},
      status: null,
      chartOptions: {
        chart: {
          id: "Workplace Morale",
        },
        xaxis: {
          categories: [],
        },
      },
      series: [
        {
          name: "average",
          data: [],
        },
      ],
    };
  },
  //mounted: function () {
  // axios.get("/reports").then((response) => {
  // (reports = response.data),
  // (dateList = []),
  // (gdbd = []),
  // reports.each(function (report) {
  //   datelist.push(report.date);
  //  })((chartOptions.xaxis.catagories = [...new Set(datelist)]));
  //  });

  //TODO: pull Data(dates and GDBD's)
  //TODO: get de-duped dates list/array from data
  //TODO: get and average GDBD per each date
  //TODO: set dates to chartOprions.xaxis.catagories
  //TODO: set averages to chartOptions.series.data
  // },
  created: function () {
    this.indexReports();
  },
  methods: {
    isAdmin: function () {
      return localStorage.getItem("admin").toLowerCase() == "true";
    },
    indexReports: function () {
      axios.get("/reports").then((response) => {
        this.reports = response.data;
        console.log(this.reports);
      });
    },
    showReport: function () {
      var params = {
        report_id: this.report_id.id,
      };
      axios
        .get("/reports", params)
        .then((response) => {
          console.log("get it", response);
          this.$router.push("/ShowReport");
        })
        .catch((error) => {
          console.log("get it error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
