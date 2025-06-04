<template>
  <div id="exam-results">
    <img src="/media/exam/resultNote.png" alt="note" class="note" />
    <div class="text-container">
      <p class="header">התוצאות של {{this.fullName}}</p>
      <p>ציון:</p>
      <p class="back-btn" @click="backToQues">מעבר על המבחן</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "exam-results",
  props: ['fullName'],
  data() {
    return {};
  },
  methods: {
    backToQues() {
 this.$emit('back-to-ques');
    },
  },
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
  transform: translate(-50%, -50%) rotate(-8deg);
}

.back-btn {
  z-index: 1;

  width: 10rem;
  height: 3rem;
  font-size: 1rem;
  background-color: #8cd0ec;
  border-radius: 1.5rem;
  padding: 0; /* Remove padding to ensure centering works properly */
  /* Centering the text */
  display: flex;
  justify-content: center; /* Horizontally centers the text */
  align-items: center; /* Vertically centers the text */
  text-align: center; /* Ensures the text is centered if multiline */
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
