<template>
  <div id="exam">
    <exam-questions
      v-show="!showResults"
      @show-results="showTheResults"
      :checkAns="checkAns"
      :numQues="numCurrentQues"
      @change-current-num-ques="changeCurrentNumQues"
    ></exam-questions>
    <exam-results
      :fullName="fullName"
      :score="score"
      :counterCorrect="counterCorrect"
      :numQuestions="numQuestions"
      v-show="showResults"
      @back-to-ques="BackToQues"
      :counterDoOvers="counterDoOvers"
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
      checkAns: false,
      score: 0,
      counterCorrect: 0,
      numQuestions: 0,
      numCurrentQues: 0,
      counterDoOvers: 0,
    };
  },
  methods: {
    changeCurrentNumQues(theChange) {
      if (typeof theChange !== "boolean") {
        this.numCurrentQues = theChange;
      } else if(theChange) {
        this.numCurrentQues++;
      } else {
        this.numCurrentQues--;
      }
    },

    showTheResults(s, c, n) {
      this.checkAns = true;
      this.showResults = true;
      this.score = Math.round(s);
      this.counterCorrect = c;
      this.numQuestions = n;
    },
    BackToQues() {
      this.numCurrentQues = 0;
      this.showResults = false;
      
      if (this.score < 70) {
        //אם עשה כבר 2 ניסיונות חוזרים עליו ללמוד מחדש את הלומדה
        if(this.counterDoOvers === 2) {
          window.location.reload();
        } else {
          this.checkAns = false;
        this.counterDoOvers++;
        }
        
      } 
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
