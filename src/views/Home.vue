<template>
  <div class="Home">
    <div class="card card-primary">
      <div class="card-header">
        <h3 class="card-title">Workplace MoralE</h3>

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
        <li class="page-item">
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
        <li class="page-item active">
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
                </tr>
              </thead>
              <tbody>
                <tr v-for="report in reports" v-bind:key="report.id">
                  <td>{{ report.good_day_bad_day }}</td>
                  <td>
                    <router-link v-bind:to="`/reports/${report.id}`">{{ report.Date }}</router-link>
                  </td>
                  <td>
                    <span
                      class="badge badge-success"
                      :class="
                        report.worked < 8 ? 'badge-warning' : report.worked > 8 ? 'badge-danger' : 'badge-success'
                      "
                      v-bind:key="report.worked"
                    >
                      {{ report.worked }}
                    </span>
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
      status: null,
      dateList: [],
      gdbd: [],
      totalPrinted: [],
      totalCut: [],
      chartOptions: {
        chart: {
          id: "Workplace Morale",
        },
        xaxis: {
          type: "datetime",
          categories: [], //["7.1.2021", "7.2.2021", "7.3.2021", "7.4.2021", "7.5.2021", "7.6.2021"],
        },
      },
      series: [
        {
          name: "series-1",
          data: [], //[30, 40, 35, 50, 49, 60, 70, 500],
        },
      ],
      series2: [
        {
          name: "series-2",
          data: [], //[30, 40, 35, 50, 49, 60, 70, 500],
        },
      ],
    };
  },
  mounted: function () {
    //TODO: pull Data(dates and GDBD's)
    //TODO: get de-duped dates list/array from data
    //TODO: get and average GDBD per each date
    //TODO: set dates to chartOprions.xaxis.catagories
    //TODO: set averages to chartOptions.series.data
  },
  created: function () {
    this.indexReports();
  },
  methods: {
    pullInfo: function () {
      let dataset = [];
      this.reports.forEach((report) => {
        if (
          this.chartOptions.xaxis.categories.length > 0 &&
          this.chartOptions.xaxis.categories[this.chartOptions.xaxis.categories.length - 1] === report.Date
        ) {
          console.log("dies this ever happen:");
          dataset[dataset.length - 1] += report.printed;
        } else {
          this.chartOptions.xaxis.categories.push(report.Date);
          dataset.push(report.printed);
        }
      });
      this.series[0].data = dataset;
    },

    isAdmin: function () {
      return localStorage.getItem("admin").toLowerCase() == "true";
    },
    indexReports: function () {
      axios.get("/reports").then((response) => {
        this.reports = response.data.sort((a, b) => {
          if (a.Date < b.Date) {
            return -1;
          }
          if (a.Date > b.Date) {
            return 1;
          }
          return 0;
        });

        console.log(this.reports);
        this.pullInfo();
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
