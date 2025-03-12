<template>
  <div id="app">
    <clouds-bg class="clouds-bg"></clouds-bg>
    <img
      class="bahadSymbol"
      src="../src/assets/media/bahadSymbol.png"
      alt="bahadSymbol"
    />
    <img
      @click="toHomePage"
      v-if="part > 0"
      class="homeIcon"
      src="../src/assets/media/homeIcon.png"
      alt="homeIcon"
    />
    <open-page
      :showSelection="showSelection"
      @to-study="showStartSign"
      @theChosenCourse="updateChosenCourse"
      v-if="part === 0"
    ></open-page>
    <start-sign
      :partNum="partNum"
      :firstChosen="firstChosen"
      @toNextBoard="nextPart"
      v-if="part === 1"
    ></start-sign>
    <info-screen :chosenCourse="chosenCourse" :navPart="partNum" v-if="part === 2"></info-screen>
  </div>
</template>

<script>
import CloudsBg from "./components/CloudsBg.vue";
import InfoScreen from "./components/InfoScreen.vue";
import OpenPage from "./components/OpenPage.vue";
import StartSign from "./components/StartSign.vue";
export default {
  name: "app",
  components: {
    OpenPage,
    InfoScreen,
    StartSign,
    CloudsBg,
  },
  data() {
    return {
      part: 0,
      partNum: -1,
      firstChosen: null,
      showSelection: false,
      chosenCourse: '',
      // navPart: -1,
    };
  },
  methods: {
    showStartSign(fChosen, studyPart) {
      this.partNum = studyPart;
      this.firstChosen = fChosen;
      this.part++;
    },
    toHomePage() {
      console.log('hi');
      this.part = 0;
      this.showSelection = true;
    },
    nextPart() {
      this.part++;
    },
    updateChosenCourse(chosenCrane) {
      this.chosenCourse = chosenCrane;
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
  /* display: grid; */
}

.bahadSymbol {
  width: 4rem;
  position: absolute;
  top: 1rem;
  left: 1rem;
  z-index: 2;
}

.homeIcon {
  position: absolute;
  right: 1rem;
  top: 1rem;
  width: 2.5rem;
  cursor: pointer;
  z-index: 2;
}
@media screen and (max-width: 600px) {
  .homeIcon {
    display: none;
  }

  .bahadSymbol {
    width: 3rem;
    top: 0.5rem;
  }
}
</style>
