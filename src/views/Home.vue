<template>
  <div class="Home">
    <!-- AREA CHART -->
    <div class="card card-primary">
      <div class="card-body">
        <div class="chart">
          <canvas id="areaChart" style="min-height: 250px; height: 250px; max-height: 250px; max-width: 100%"></canvas>
        </div>
      </div>
      <!-- /.card-body -->
    </div>
    <div class="row">
      <div class="card">
        <div class="card-header border-transparent">
          <h3 class="card-title">
            <p v-if="current_user.admin === true">All Reports</p>
            <p v-if="current_user.admin === false">My Reports</p>
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
    </div>
  </div>
</template>

<script>
/* global $, Chart */
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
    this.indexReports();
  },
  mounted: function () {
    $(function () {
      /* ChartJS
       * -------
       * Here we will create a few charts using ChartJS
       */

      //--------------
      //- AREA CHART -
      //--------------

      // Get context with jQuery - using jQuery's .get() method.
      var areaChartCanvas = $("#areaChart").get(0).getContext("2d");

      var areaChartData = {
        labels: ["February", "March", "April", "May", "June", "July"],
        datasets: [
          {
            label: "Digital Goods",
            backgroundColor: "rgba(60,141,188,0.9)",
            borderColor: "rgba(60,141,188,0.8)",
            pointRadius: false,
            pointColor: "#3b8bba",
            pointStrokeColor: "rgba(60,141,188,1)",
            pointHighlightFill: "#fff",
            pointHighlightStroke: "rgba(60,141,188,1)",
            data: [28, 48, 40, 19, 86, 27, 90],
          },
          {
            label: "Electronics",
            backgroundColor: "rgba(210, 214, 222, 1)",
            borderColor: "rgba(210, 214, 222, 1)",
            pointRadius: false,
            pointColor: "rgba(210, 214, 222, 1)",
            pointStrokeColor: "#c1c7d1",
            pointHighlightFill: "#fff",
            pointHighlightStroke: "rgba(220,220,220,1)",
            data: [65, 59, 80, 81, 56, 55, 40],
          },
        ],
      };

      var areaChartOptions = {
        maintainAspectRatio: false,
        responsive: true,
        legend: {
          display: false,
        },
        scales: {
          xAxes: [
            {
              gridLines: {
                display: false,
              },
            },
          ],
          yAxes: [
            {
              gridLines: {
                display: false,
              },
            },
          ],
        },
      };

      // This will get the first returned node in the jQuery collection.
      new Chart(areaChartCanvas, {
        type: "line",
        data: areaChartData,
        options: areaChartOptions,
      });

      //-------------
      //- LINE CHART -
      //--------------
      // var lineChartCanvas = $("#lineChart").get(0).getContext("2d");
      var lineChartOptions = $.extend(true, {}, areaChartOptions);
      var lineChartData = $.extend(true, {}, areaChartData);
      lineChartData.datasets[0].fill = false;
      lineChartData.datasets[1].fill = false;
      lineChartOptions.datasetFill = false;

      //var lineChart = new Chart(lineChartCanvas, {
      // type: "line",
      // data: lineChartData,
      //  options: lineChartOptions,
      // });

      //-------------
      //- DONUT CHART -
      //-------------
      // Get context with jQuery - using jQuery's .get() method.
      var donutChartCanvas = $("#donutChart").get(0).getContext("2d");
      var donutData = {
        labels: ["Chrome", "IE", "FireFox", "Safari", "Opera", "Navigator"],
        datasets: [
          {
            data: [700, 500, 400, 600, 300, 100],
            backgroundColor: ["#f56954", "#00a65a", "#f39c12", "#00c0ef", "#3c8dbc", "#d2d6de"],
          },
        ],
      };
      var donutOptions = {
        maintainAspectRatio: false,
        responsive: true,
      };
      //Create pie or douhnut chart
      // You can switch between pie and douhnut using the method below.
      new Chart(donutChartCanvas, {
        type: "doughnut",
        data: donutData,
        options: donutOptions,
      });

      //-------------
      //- PIE CHART -
      //-------------
      // Get context with jQuery - using jQuery's .get() method.
      var pieChartCanvas = $("#pieChart").get(0).getContext("2d");
      var pieData = donutData;
      var pieOptions = {
        maintainAspectRatio: false,
        responsive: true,
      };
      //Create pie or douhnut chart
      // You can switch between pie and douhnut using the method below.
      new Chart(pieChartCanvas, {
        type: "pie",
        data: pieData,
        options: pieOptions,
      });

      //-------------
      //- BAR CHART -
      //-------------
      var barChartCanvas = $("#barChart").get(0).getContext("2d");
      var barChartData = $.extend(true, {}, areaChartData);
      var temp0 = areaChartData.datasets[0];
      var temp1 = areaChartData.datasets[1];
      barChartData.datasets[0] = temp1;
      barChartData.datasets[1] = temp0;

      var barChartOptions = {
        responsive: true,
        maintainAspectRatio: false,
        datasetFill: false,
      };

      new Chart(barChartCanvas, {
        type: "bar",
        data: barChartData,
        options: barChartOptions,
      });

      //---------------------
      //- STACKED BAR CHART -
      //---------------------
      var stackedBarChartCanvas = $("#stackedBarChart").get(0).getContext("2d");
      var stackedBarChartData = $.extend(true, {}, barChartData);

      var stackedBarChartOptions = {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          xAxes: [
            {
              stacked: true,
            },
          ],
          yAxes: [
            {
              stacked: true,
            },
          ],
        },
      };

      new Chart(stackedBarChartCanvas, {
        type: "bar",
        data: stackedBarChartData,
        options: stackedBarChartOptions,
      });
    });
  },
  methods: {
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
          console.log("sget it error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
