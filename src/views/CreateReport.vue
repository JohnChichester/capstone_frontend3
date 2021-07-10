<template>
  <div class="csidebar-mini sidebar-closed sidebar-collapse" style="height: auto">
    <div class="content-header"></div>
    <div class="card card-primary">
      <div class="card-header">
        <h3 class="card-title">EOD</h3>

        <div class="card-tools">
          <button type="button" class="btn btn-tool" data-card-widget="collapse" title="Collapse">
            <i class="fas fa-minus"></i>
          </button>
        </div>
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="submit()">
          <div class="form-group">
            <label for="question.good_day_bad_day">How was your day?</label>
            <select id="inputStatus" class="form-control custom-select">
              <option selected disabled>Select one</option>
              <option for="1">Great</option>
              <option for="0">Fine</option>
              <option for="-1">Not So Good</option>
            </select>
          </div>

          <!-- -->
          <div class="form-group" v-for="question in questions" v-bind:key="question.id">
            <label for="question.catagory">{{ question.question_text }}</label>
            <textarea class="form-control" rows="4" type="text" v-model="question.catagory"></textarea>
          </div>
          <!-- -->
          <div class="form-group">
            <label for="misc">Misc tracking was due to..</label>
            <input type="text" id="misc" class="form-control" v-model="misc" />
          </div>
          <div class="form-group">
            <label for="worked">Hours Worked</label>
            <input type="integer" id="worked" class="form-control" v-model="worked" />
          </div>
          <div class="form-group">
            <label for="misc">Square foot printed</label>
            <input type="integer" id="printed" class="form-control" v-model="printed" />
          </div>
          <div class="form-group">
            <label for="misc">Square foot cut</label>
            <input type="integer" id="cut" class="form-control" v-model="cut" />
          </div>
          <input type="submit" value="Submit" />
        </form>
      </div>
      <!-- /.card-body -->
    </div>
    <!-- /.card -->

    <form v-on:submit.prevent="submit()">
      <div class="card card-default">
        <h1></h1>
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <div>
          <label>How was your day?</label>
          <input type="integer" v-model="good_day_bad_day" />
        </div>
        <div v-for="question in questions" v-bind:key="question.id">
          <label>{{ question.question_text }}</label>
          <input type="text" v-model="question.catagory" />
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
      </div>
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
      version: 1,
      questions: [],
    };
  },
  created: function () {
    this.indexQuestions();
    //console.log("this.questions");
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
        version: this.version,
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
    indexQuestions: function () {
      var params = {
        version: 0,
      };
      axios.get("/questions", params).then((response) => {
        console.log("this.questions", response);
        this.questions = response.data;
      });
    },
  },
};
</script>
