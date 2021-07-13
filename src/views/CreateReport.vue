<template>
  <div class="csidebar-mini sidebar-closed sidebar-collapse" style="height: auto">
    <div class="content-header"></div>
    <div class="card card-primary">
      <div class="card-header">
        <h3 class="card-title">Extra Ess EOD</h3>

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
            <select id="inputStatus" class="form-control custom-select" v-model="good_day_bad_day">
              <option selected disabled>Select one</option>
              <option value="1">Great</option>
              <option value="0">Fine</option>
              <option value="-1">Not So Good</option>
            </select>
          </div>

          <div class="form-group">
            <label for="safety">Are there any safety concerns?</label>
            <textarea class="form-control" rows="4" type="text" v-model="safety"></textarea>
          </div>
          <div class="form-group">
            <label for="sustain">Did you leave your workspace in better condition than when you arrived?</label>
            <textarea class="form-control" rows="4" type="text" v-model="sustain"></textarea>
          </div>
          <div class="form-group">
            <label for="shine">
              Report of Quality Issues, Concerns for Review (All materials have nice clean edges and are neatly stacked
              on pallets):
            </label>
            <textarea class="form-control" rows="4" type="text" v-model="shine"></textarea>
          </div>
          <div class="form-group">
            <label for="sort">Was your schedule completed and work tracked accurately?</label>
            <textarea class="form-control" rows="4" type="text" v-model="sort"></textarea>
          </div>
          <div class="form-group">
            <label for="set_in_order">Was the needed material tagged properly for production?</label>
            <textarea class="form-control" rows="4" type="text" v-model="set_in_order"></textarea>
          </div>
          <div class="form-group">
            <label for="standardize">
              Did you receive job bags that were properly signed and contained all needed items for production?
            </label>
            <textarea class="form-control" rows="4" type="text" v-model="standardize"></textarea>
          </div>
          <!-- 
          <div class="form-group" v-for="question in questions" v-bind:key="question.id">
            <label for="question.catagory">{{ question.question_text }}</label>
            <textarea class="form-control" rows="4" type="text" v-model="question.catagory"></textarea>
          </div>
           -->
          <!-- 
          <div class="form-group" v-for="question in questions" v-bind:key="question.id">
            <label for="question.catagory">{{ question.question_text }}</label>
            <textarea class="form-control" rows="4" type="text" v-model="question.catagory"></textarea>
          </div>
           -->

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
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      good_day_bad_day: 0,
      safety: "",
      sustain: "",
      shine: "",
      sort: "",
      set_in_order: "",
      standardize: "",
      misc: "",
      worked: 8,
      printed: 0,
      cut: 0,
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
        worked: this.worked,
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
