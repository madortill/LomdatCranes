<template>
  <div id="exam">
    <exam-questions
      v-show="!showResults"
      @show-results="showTheResults"
    ></exam-questions>
    <exam-results
      :fullName="fullName"
      :score="score"
      :counterCorrect="counterCorrect"
      :numQuestions="numQuestions"
      v-show="showResults"
      @back-to-ques="BackToQues"
    ></exam-results>
  </div>
</template>

<script>
import ExamQuestions from "./ExamQuestions.vue";
import ExamResults from "./ExamResults.vue";
export default {
  components: { ExamQuestions, ExamResults },
  name: "exam",
  props: ["idNumber", "fullName"],
  data() {
    return {
      showResults: false,
      score: 0,
      counterCorrect: 0,
      numQuestions: 0,
    };
  },
  methods: {
    showTheResults(s, c, n) {
      this.showResults = true;
      this.score = Math.round(s);
      this.counterCorrect = c;
      this.numQuestions = n;
    },
    BackToQues() {
      this.showResults = false;
    },
  },
};
</script>

<style scoped>
#exam {
  width: 100vw;
  height: 100vh;
  z-index: 1;
}

@media screen and (max-width: 600px) {
  #exam {
    width: 100vw;
    height: 91vh;
  }
}
</style>
