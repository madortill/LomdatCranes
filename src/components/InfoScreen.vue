<template>
  <div id="info-screen">
    <img
      @click="toHomePage"
      class="homeIcon"
      :style="{ '--home-icon-color': colorIconPhone }"
      src="../assets/media/homeIcon.png"
      alt="homeIcon"
    />
    <start-sign
      :sectionNum="sectionToStudy"
      :firstChosen="firstChosen"
      :thePart="thePart"
      @to-next-board="nextInStartSign"
      @to-prev-board="backToStartSign"
      v-if="partToShow === 0"
    ></start-sign>
    <navbar
      :part="sectionToStudy"
      :subjNum="subNavPart"
      v-if="partToShow > 0"
    ></navbar>

    <general-material
      v-if="sectionToStudy === 0 && showTheSection"
      @back-to-start-sign="backToStartSign"
      @toHomePage="toHomePage"
      :navbarSubjNum="subNavPart"
      @change-sub-nav-num="changeSubNavNum"
      :chosenCourse="chosenCourse"
    ></general-material>
  </div>
</template>

<script>
import GeneralMaterial from "./GeneralMaterial.vue";
import Navbar from "./Navbar.vue";
import StartSign from "./StartSign.vue";
export default {
  name: "info-screen",
  components: { Navbar, StartSign, GeneralMaterial },
  props: ["chosenCourse", "firstChosen", "sectionToStudy", "colorIconPhone"],
  data() {
    return {
      partToShow: 0,
      thePart: 0,

      Infopart: 1,
      infoHangingPart: 0,
      subNavPart: 1,
      showTheSection: false,
      //about the flip according to click
      flipStart: false,
      flipEndDefine: false,
      backFlip: false,
      flipEndSaftyRules: false,
      showNextBtn: true,
      seenSafetyRules: false,
      //aboutCarousel
      prevToCarousel: false,
      craneCardClicked: false,
      titleTypesCranesIndex: "סוגי העגורנים הקיימים",
    };
  },
  methods: {
    //מראה חלק הבא בקומפוננטת StartSign או שמעביר לחלק של הלמידה שהמשתמש בחר
    nextInStartSign() {
      if (this.sectionToStudy === 0 && this.thePart === 0) {
        this.thePart++;
      } else {
        this.showTheSection = true;
        this.partToShow++; //shows now the navbar
      }
    },
    //מחזיר לקומפוננטה StartSign או שעושה חזור בקומפוננטה עצמה
    backToStartSign() {
      if (this.showTheSection) {
        this.showTheSection = false;
        this.partToShow--;
        this.thePart = 1;
      } else {
        this.thePart--;
      }
    },
    toHomePage() {
      this.$emit("toHomePage");
    },
    showNextBtnSafetyRules() {
      this.showNextBtn = true;
      this.seenSafetyRules = true;
    },
    CraneCardChosen(craneTitle) {
      this.prevToCarousel = true;
      this.craneCardClicked = true;
      this.titleTypesCranesIndex = craneTitle;
    },
    changeSubNavNum(isUp) {
      if (isUp) {
        this.subNavPart++;
      } else {
        this.subNavPart--;
      }
    },
  },
};
</script>

<style scoped>
#info-screen {
  z-index: 7;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.fix-layer {
  z-index: 1;
}

.homeIcon {
  position: absolute;
  right: 1rem;
  top: 1rem;
  width: 2.5rem;
  cursor: pointer;
  z-index: 3;
}

@media screen and (max-width: 600px) {
  .homeIcon {
    filter: var(--home-icon-color);
    right: auto;
    left: 4.6rem;
  }
}
</style>
