<template>
  <div id="exam">
<exam-questions></exam-questions>
  </div>
</template>

<script>
import ExamQuestions from './ExamQuestions.vue';
export default {
  components: { ExamQuestions },
  name: "exam",
  props: [],
  data() {
    return {
  
    };
  },
  methods: {

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
