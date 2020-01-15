<template>
  <div>
    <Header :numCorrect="numCorrect" :numTotal="numTotal" />
    <div class="div">Timer: {{ countDown }}</div>
    <div v-if="countDown === 0" class="cons">Times up</div>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="10" offset="1">
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "../components/Header.vue";
import QuestionBox from "../components/QuestionBox";
import { setTimeout } from "timers";

export default {
  name: "GamePlay",
  components: {
    QuestionBox,
    Header
  },
  props: {
    apiObject: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      countDown: null,
      selectedCategoryOption: null
    };
  },
  methods: {
    log(x) {
      this.selectedCategoryOption = x;
    },
    state() {
      if (this.countDown === 0) {
        // disable eslint no-console
        // console.log("zero");
      }
    },
    reset() {
      this.countDown = null;
      this.countDown = 10;
    },
    next() {
      this.index++;
      this.reset();
      // this.countDown = 10
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    },
    countDownTimer() {
      if (this.countDown > 0) {
        setTimeout(() => {
          this.countDown -= 1;
          this.countDownTimer();
        }, 1000);
      }
    }
  },
  mounted: function() {
    fetch(
      `https://opentdb.com/api.php?amount=${this.apiObject.apiAmount}&category=${this.apiObject.apiCategory.id}&difficulty=${this.apiObject.apiDifficulty}&type=${this.apiObject.apiType}`,
      {
        method: "get"
      }
    )
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        this.questions = jsonData.results;
        this.reset();
        this.countDownTimer();
      });
  }
};
</script>
