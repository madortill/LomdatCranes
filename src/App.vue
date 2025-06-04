<template>
  <div id="app">
    <clouds-bg v-if="showCloudsBg" class="clouds-bg"></clouds-bg>

    <img
      class="bahadSymbol"
      src="../src/assets/media/bahadSymbol.png"
      alt="bahadSymbol"
    />

    <open-page
      :showSelection="showSelection"
      @to-study="showChosenSection"
      @theChosenCourse="updateChosenCourse"
      v-if="partNum === 0"
      :indexYellowSign="indexYellowSign"
      @next-index-yellow-sign="nextIndexYellowSign"
      :ableExam="ableExam"
    ></open-page>

    <info-screen
      :firstChosen="firstChosen"
      :chosenCourse="chosenCourse"
      v-if="partNum === 1"
      :sectionToStudy="sectionToStudy"
      @toHomePage="toHomePage"
      @to-show-cloud-bg="toShowCloudBg"
      @next-section-to-study="finishedGeneralMaterial"
      @prev-studied-section="prevStudiedSection"
      @finished-operation="finishedOperation"
    ></info-screen>
  </div>
</template>

<script>
import CloudsBg from "./components/CloudsBg.vue";
import InfoScreen from "./components/InfoScreen.vue";
import OpenPage from "./components/OpenPage.vue";
export default {
  name: "app",
  components: {
    OpenPage,
    InfoScreen,
    CloudsBg,
  },
  data() {
    return {
      partNum: 0,
      sectionToStudy: -1,
      firstChosen: null,
      showSelection: false,
      chosenCourse: "",
      indexYellowSign: 0,
      showCloudsBg: true,
      finishedLearnedBoxes: [false, false],
      ableExam: true,
    };
  },
  methods: {
    showChosenSection(fChosen, studyPart) {
      this.sectionToStudy = studyPart;
      this.firstChosen = fChosen;
      this.partNum++;
    },
    toHomePage() {
      this.partNum = 0;
      this.showSelection = true;
    },

    updateChosenCourse(chosenCrane) {
      this.chosenCourse = chosenCrane;
    },

    nextIndexYellowSign() {
      this.indexYellowSign++;
    },
    toShowCloudBg(show) {
      if (show) {
        this.showCloudsBg = true;
      } else {
        this.showCloudsBg = false;
      }
    },
    finishedGeneralMaterial() {
      this.sectionToStudy++;
      this.firstChosen = false;
      this.finishedLearnedBoxes[0] = true;
        this.toShowTheExam();
      
    },

    finishedOperation() {
      this.finishedLearnedBoxes[1] = true;
      this.toShowTheExam();
    },

    toShowTheExam() {
      if (this.finishedLearnedBoxes[0] && this.finishedLearnedBoxes[1]) {
        this.ableExam = true;
      }
    },

    prevStudiedSection() {
      this.sectionToStudy--;
      this.firstChosen = true;
    },
  },
};
</script>

<style>
@font-face {
  font-family: "Heebo";
  src: url("@/assets/fonts/heebo.regular.ttf");
}

@font-face {
  font-family: "Heebo-Bold";
  src: url("@/assets/fonts/heebo.black.ttf");
}

@font-face {
  font-family: "Secular-One";
  src: url("@/assets/fonts/SecularOne-Regular.ttf");
}

* {
  overflow: hidden;
  font-family: "Heebo";
}

:root {
  font-size: calc(10px + 0.5vw);
}

body {
  margin: 0;
  direction: rtl;
  background-color: #f2f2f2;
  overflow: hidden;
}

#app {
  font-family: "Heebo";
  width: 100vw;
  height: 100vh;
  position: relative;
  text-align: center;
  background-color: #e0f2f4;
  font-size: 1.2rem;
}

.bahadSymbol {
  width: 4rem;
  position: absolute;
  top: 1rem;
  left: 1rem;
  z-index: 3;
}

@media screen and (max-width: 600px) {
  .bahadSymbol {
    width: 2.4rem;
    top: 0.5rem;
  }
  
  body {
    height: 91vh;
    overflow: hidden;
  }

  #app {
    height: 91vh;
  }
}
</style>
