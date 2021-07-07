<template>
  <div class="content-wrapper">
    <div class="content-header">
      <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#modal-primary">
        Create New Report
      </button>
    </div>
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h4 class="modal-title">How Was Your Day?</h4>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">×</span>
          </button>
        </div>
        <div class="modal-body">
          <a class="btn btn-app bg-success">
            <i class="fa-regular fa-face-smile-beam"></i>
            <p>Good</p>
          </a>
          <a class="btn btn-app bg-warning">Fine</a>
          <a class="btn btn-app bg-danger">
            <i class="fa-regular fa-face-frown"></i>
            Bad
          </a>
        </div>
        <div class="modal-footer justify-content-between">
          <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
      <!-- /.modal-content -->
    </div>
    <form v-on:submit.prevent="submit()">
      <h1>Create Report</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>How was your day?</label>
        <input type="integer" v-model="good_day_bad_day" />
      </div>
      <div>
        <label>Safety</label>
        <input type="text" v-model="safety" />
      </div>
      <div>
        <label>Sustain</label>
        <input type="text" v-model="sustain" />
      </div>
      <div>
        <label>Shine</label>
        <input type="text" v-model="shine" />
      </div>

      <div>
        <label>Sort</label>
        <input type="text" v-model="sort" />
      </div>
      <div>
        <label>Set in order</label>
        <input type="text" v-model="set_in_order" />
      </div>
      <div>
        <label>Standardize</label>
        <input type="text" v-model="standardize" />
      </div>
      <div>
        <label>Misc</label>
        <input type="text" v-model="misc" />
      </div>
      <div>
        <label>Hours Worked</label>
        <input type="integer" v-model="worked" />
      </div>
      <div>
        <label>Square foot printed</label>
        <input type="integer" v-model="printed" />
      </div>
      <div>
        <label>Square foot cut</label>
        <input type="integer" v-model="cut" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      good_day_bad_day: "",
      safety: "",
      sustain: "",
      shine: "",
      sort: "",
      set_in_order: "",
      standardize: "",
      misc: "",
      worked: 8,
      printed: "",
      cut: "",
      errors: [],
    };
  },
  methods: {
    submit: function () {
      var params = {
        good_day_bad_day: this.good_day_bad_day,
        safety: this.safety,
        sustain: this.sustain,
        shine: this.shine,
        sort: this.sort,
        set_in_order: this.set_in_order,
        standardize: this.standardize,
        misc: this.misc,
        worked: 8,
        printed: this.printed,
        cut: this.cut,
      };
      axios
        .post("/reports", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
