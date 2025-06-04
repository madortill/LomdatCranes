<template>
  <div id="exam">
<exam-questions v-show="!showResults" @show-results="showTheResults"></exam-questions>
<exam-results :fullName="fullName" v-show="showResults" @back-to-ques="BackToQues"></exam-results>
  </div>
</template>

<script>
import ExamQuestions from './ExamQuestions.vue';
import ExamResults from './ExamResults.vue';
export default {
  components: { ExamQuestions, ExamResults },
  name: "exam",
  props: ['idNumber', 'fullName'],
  data() {
    return {
  showResults: false,
    };
  },
  methods: {
    showTheResults() {
      this.showResults = true;
    },
    BackToQues() {
      this.showResults = false;

    }
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
