<template>
  <div class="Home">
    <div class="card card-primary">
      <div class="card-header">
        <h3 class="card-title">Print & Cut Output</h3>

        <div class="card-tools">
          <button type="button" class="btn btn-tool" data-card-widget="collapse">
            <i class="fas fa-minus"></i>
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

    <div class="row justify-content-center">
      <div class="card card-primary">
        <div class="card-header">
          <h3 class="card-title">
            <p v-if="isAdmin()">All Reports</p>
            <p v-if="!isAdmin()">My Reports</p>
            <!-- <div>
              Specify Date
              <input type="text" v-model="searchFilter" list="report-dates" />
              <datalist id="report-dates">
                <select id="inputStatus" class="form-control custom-select" v-model="searchFilter">
                  <option selected disabled>View Specific Date</option>
                  <option v-for="report in reports" v-bind:key="report.date">{{ report.date }}</option>
                </select>
              </datalist>
            </div> -->
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
                  <td>
                    <p v-if="report.good_day_bad_day === 1">😀</p>
                    <p v-if="report.good_day_bad_day === -1">︁😡</p>
                    <p v-if="report.good_day_bad_day === 0">︁😐︁</p>
                  </td>
                  <td>
                    <button
                      type="button"
                      class="btn btn-block btn-outline-secondary btn-xs"
                      v-bind:to="`/reports/${report.id}`"
                    >
                      <router-link v-bind:to="`/reports/${report.id}`">{{ report.Date }}</router-link>
                    </button>
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
      <div class="card card-primary">
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
                  <td>{{ totalPrint }}</td>
                  <td>Sq Ft Printed</td>
                </tr>
                <tr>
                  <td>{{ totalCut }}</td>
                  <td>Sq Ft Cut</td>
                </tr>
                <tr>
                  <td>{{ hours }}</td>
                  <td>Total Hours</td>
                </tr>
                <tr>
                  <td>{{ overtime }}</td>
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
      totalPrint: 0,
      totalCut: 0,
      hours: 0,
      overtime: 0,
      chartOptions: {
        chart: {
          id: "Production Totals",
        },
        xaxis: {
          type: "datetime",
          categories: [],
        },
      },
      series: [
        {
          name: "printed",
          data: [],
        },
        {
          name: "cut",
          data: [],
        },
      ],
    };
  },
  //TODO: get and average GDBD per each date

  //TODO: set averages to chartOptions.series.data

  created: function () {
    this.indexReports();
  },
  methods: {
    pullInfo: function () {
      let printAmounts = [];
      let cutAmounts = [];
      this.reports.forEach((report) => {
        if (
          this.chartOptions.xaxis.categories.length > 0 &&
          this.chartOptions.xaxis.categories[this.chartOptions.xaxis.categories.length - 1] === report.Date
        ) {
          printAmounts[printAmounts.length - 1] += report.printed;
          cutAmounts[cutAmounts.length - 1] += report.cut;
        } else {
          this.chartOptions.xaxis.categories.push(report.Date);
          printAmounts.push(report.printed);
          cutAmounts.push(report.cut);
        }
        this.hours += report.worked;
        if (report.worked > 8) {
          this.overtime += report.worked - 8;
        }
      });
      console.log("hours", this.hours);
      this.series[0].data = printAmounts;
      this.series[1].data = cutAmounts;
      cutAmounts.forEach((cutDay) => {
        this.totalCut += cutDay;
      });
      printAmounts.forEach((printDay) => {
        this.totalPrint += printDay;
      });
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

        this.pullInfo();
        this.pageView();
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
