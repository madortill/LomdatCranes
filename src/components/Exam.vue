<template>
  <div id="exam">
<exam-questions v-show="!showResults" @show-results="showTheResults"></exam-questions>
<exam-results v-show="showResults"></exam-results>
  </div>
</template>

<script>
import ExamQuestions from './ExamQuestions.vue';
import ExamResults from './ExamResults.vue';
export default {
  components: { ExamQuestions, ExamResults },
  name: "exam",
  props: [],
  data() {
    return {
  showResults: false,
    };
  },
  methods: {
    showTheResults() {
      this.showResults = true;
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
