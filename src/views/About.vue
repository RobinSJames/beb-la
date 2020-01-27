<template>
  <div class="about">
    <NavBar></NavBar>
    <Header :numCorrect="numCorrect" :numTotal="numTotal" />
    <div class="div">Timer: {{ countDown }}</div>
    <div v-if="countDown === 0" class="cons">Times up</div>
    <b-container class="bv-example-row">
      <b-row class="justify-content-center">
        <b-col sm="10" md="12" offset="0">
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
import NavBar from "@/components/NavBar";

import Header from "../components/Header.vue";
import QuestionBox from "../components/QuestionBox";

export default {
  name: "app",
  components: {
    QuestionBox,
    Header,
    NavBar
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      countDown: 10,
      selectedCategoryOption: null,
      response_code: null
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function() {
    fetch(
      `https://opentdb.com/api.php?amount=${this.$attrs.apiAmount}&category=${this.$attrs.apiCategory.id}&difficulty=${this.$attrs.apiDifficulty}&type=${this.$attrs.apiType}`,
      {
        method: "get"
      }
    )
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        this.questions = jsonData.results;
        this.response_code = jsonData.response_code;
      });
  }
};
</script>
