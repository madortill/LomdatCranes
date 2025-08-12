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
      @show-finish-lomda-btn="showFinishLomdaBtn"
    ></exam-results>
    <p
      class="finished-exam-btn"
      @click="toFinishLomdaPage"
      v-if="showFinishBtn"
    >
      סיימתי
    </p>
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
      showFinishBtn: false,
    };
  },
  methods: {
    toFinishLomdaPage() {
      this.$emit("finished-lomda");
    },

    changeCurrentNumQues(theChange) {
      if (typeof theChange !== "boolean") {
        this.numCurrentQues = theChange;
      } else if (theChange) {
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
        if (this.counterDoOvers === 2) {
          window.location.reload();
        } else {
          this.checkAns = false;
          this.counterDoOvers++;
        }
      }
    },
    showFinishLomdaBtn() {
      this.showFinishBtn = true;
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

.finished-exam-btn {
  position: fixed;
  background-color: #8cd0ec;
  top: 0rem;
  left: 8rem;
  width: 9rem;
  height: 9rem;
  font-size: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 100%;
  font-weight: bold;
  transition: background-color 0.3s ease, color 0.3s ease;
  cursor: pointer;
  animation: blink-bg-ccbf7bdc 2s infinite ease-in-out;
}

.finished-exam-btn:hover {
  background-color: #023047;
  color: white;
}

@keyframes blink-bg {
  0% {
    background-color: #8cd0ec;
  }
  50% {
    background-color: #feb758;
  }
  100% {
    background-color: #8cd0ec;
  }
}

@media screen and (max-width: 600px) {
  #exam {
    width: 100vw;
    height: 91vh;
  }
}
</style>
