<template>
  <div id="exam-results">
    <img src="/media/exam/resultNote.png" alt="note" class="note" />
    <div class="text-container">
      <p class="header"> {{ theHeader }}</p>
      <p>ציון: {{ this.score }}</p>
      <p>ענית נכון על {{ this.numQuestions + " / " + this.counterCorrect }}</p>
      <p  class="back-btn" @click="backToQues">{{ backToQuesBtnText }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "exam-results",
  props: ["fullName", "score", "counterCorrect", "numQuestions", 'counterDoOvers'],
  data() {
    return {};
  },
  methods: {
    backToQues() {
      this.$emit("back-to-ques");
    },
  },
  computed: {
    theHeader() {
      if(this.score < 70) {
        return 'אופס נכשלת ' + this.fullName + '...';
      } else {
        return 'כל הכבוד ' + this.fullName + '!';        
      }
    }, 
    backToQuesBtnText() {
      if(this.score < 70) {
        if(this.counterDoOvers === 2) {
          return 'למידה מחדש';
        } else {
          return 'נסיון חוזר';
        }
      } else {
        return 'מעבר על המבחן';        
      }
    }
  }
};
</script>

<style scoped>
#exam-results {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.note {
  height: 40rem;
}

.header {
  font-weight: bold;
  font-size: 2rem;
}

.text-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -60%) rotate(-8deg);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.back-btn {
  z-index: 1;
  width: 10rem;
  height: 3rem;
  font-size: 1rem;
  background-color: #8cd0ec;
  border-radius: 1.5rem;
  padding: 0; 
  /* Centering the text */
  display: flex;
  justify-content: center; 
  align-items: center; 
  text-align: center; 
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.back-btn:hover {
  background-color: #023047;
  color: white;
}

@media screen and (max-width: 600px) {
  #exam-results {
    width: 100vw;
    height: 91vh;
  }
}
</style>
