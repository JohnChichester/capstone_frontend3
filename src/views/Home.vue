<template>
  <div class="Home">
    <!-- AREA CHART -->
    <div class="card card-primary">
      <div class="card-body">
        <div class="chart">
          <div class="chartjs-size-monitor">
            <div class="chartjs-size-monitor-expand"><div class=""></div></div>
            <div class="chartjs-size-monitor-shrink"><div class=""></div></div>
          </div>
          <canvas
            id="reportMood"
            style="min-height: 250px; height: 250px; max-height: 250px; max-width: 100%; display: block; width: 380px"
            width="760"
            height="500"
            class="chartjs-render-monitor"
          ></canvas>
        </div>
      </div>
      <!-- /.card-body -->
    </div>
    <div class="row">
      <div class="card">
        <div class="card-header border-transparent">
          <h3 class="card-title">
            <p v-if="current_user.admin == true">All Reports</p>
            <p v-if="current_user.admin == false">My Reports</p>
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
                    <a href="report/id/">{{ report.Date }}</a>
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
    <div v-for="report in reports" v-bind:key="report.id">
      <p>{{ report.good_day_bad_day }}</p>
      <p>{{ report.Date }}</p>
      <p>{{ report.worked }}</p>
    </div>
  </div>
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
    this.indexReports();
  },
  methods: {
    indexReports: function () {
      axios.get("/reports").then((response) => {
        this.reports = response.data;
        console.log(this.reports);
      });
    },
  },
};
</script>
