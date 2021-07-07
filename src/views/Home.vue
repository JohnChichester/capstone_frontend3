<template>
  <div class="content-wrapper">
    <!-- AREA CHART -->
    <div class="card card-primary">
      <div class="card-body">
        <div class="chart">
          <div class="chartjs-size-monitor">
            <div class="chartjs-size-monitor-expand"><div class=""></div></div>
            <div class="chartjs-size-monitor-shrink"><div class=""></div></div>
          </div>
          <canvas
            id="areaChart"
            style="min-height: 250px; height: 250px; max-height: 250px; max-width: 100%; display: block; width: 380px"
            width="760"
            height="500"
            class="chartjs-render-monitor"
          ></canvas>
        </div>
      </div>
      <!-- /.card-body -->
      <div class="card">
        <div class="card-header border-transparent">
          <h3 class="card-title">My Reports</h3>

          <div class="card-tools">
            <button type="button" class="btn btn-tool" data-card-widget="collapse">
              <i class="fas fa-minus"></i>
            </button>
            <button type="button" class="btn btn-tool" data-card-widget="remove">
              <i class="fas fa-times"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
};
</script>
