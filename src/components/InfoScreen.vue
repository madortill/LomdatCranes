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
      :showWarning="showWarning"
      @to-next-board="nextInStartSign"
      @to-prev-board="backToStartSign"
      @change-show-warning="changeShowWarning"
      v-if="partToShow === 0"
    ></start-sign>
    <navbar
      :part="sectionToStudy"
      :subjNum="subNavPart"
      v-if="partToShow === 1 && showNavbar"
    ></navbar>

    <general-material
      v-if="sectionToStudy === 0 && showTheSection && partToShow !== 2"
      @back-to-start-sign="backToStartSign"
      @toHomePage="toHomePage"
      :navbarSubjNum="subNavPart"
      @change-sub-nav-num="changeSubNavNum"
      :chosenCourse="chosenCourse"
      :colorIconPhone="colorIconPhone"
      @change-home-icon="ChangeHomeIcon"
      @show-american-ques="showAmericanQues"
      @hide-navbar="hideNavbar"
      @update-color-icon-home="updateColorIconPhone"
      @to-show-cloud-bg="toShowCloudBg"
      @finished-genearal-material="finishedMainSubjBox"
    ></general-material>
    
    <operation v-if="sectionToStudy === 1 && showTheSection && partToShow !== 2" @back-to-start-sign="backToStartSign" :navbarSubjNum="subNavPart"></operation>
  </div>
</template>

<script>
import GeneralMaterial from "./GeneralMaterial.vue";
import Navbar from "./Navbar.vue";
import Operation from './Operation.vue';
import StartSign from "./StartSign.vue";

export default {
  name: "info-screen",
  components: { Navbar, StartSign, GeneralMaterial, Operation },
  props: ["chosenCourse", "firstChosen", "sectionToStudy"],
  data() {
    return {
      partToShow: 0,
      thePart: 0,
      colorIconPhone: "none",
      showWarning: true,
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
      // indexForGeneralMaterial: 0,
      showNavbar: true,
    };
  },
  methods: {
    //מראה חלק הבא בקומפוננטת StartSign או שמעביר לחלק של הלמידה שהמשתמש בחר
    nextInStartSign() {
      if ((this.sectionToStudy === 0 || this.sectionToStudy === 1) && this.thePart === 0) {
        this.thePart++;
      } else {
        this.showTheSection = true;
        this.partToShow++; //shows now the navbar
        this.updateColorIconPhone(
          "invert(1) brightness(100%) saturate(25%) contrast(100%)"
        );
      }
    },
    //מחזיר לקומפוננטה StartSign או שעושה חזור בקומפוננטה עצמה
    backToStartSign() {
      if (this.showTheSection) {
        this.showTheSection = false;
        this.partToShow--;
        this.thePart = 1;
        this.updateColorIconPhone("none");
        this.showWarning = false;
      } else {
        this.thePart--;
      }
    },
    toHomePage() {
      this.$emit("toHomePage");
      this.colorIconPhone = "none";
    },

    updateColorIconPhone(newColor) {
      this.colorIconPhone = newColor; // Update colorIconPhone based on the child’s emitted value
    },

    changeSubNavNum(isUp) {
      if (isUp) {
        this.subNavPart++;
      } else {
        this.subNavPart--;
      }
    },

    // showAmericanQues() {
    //   this.partToShow++;
    // },
    // backFromQues() {
    //   this.partToShow--;
    // this.indexForGeneralMaterial = 1;
    // },
    // changeIndexOrderGeneralMaterial(isNext) {
    //   if(isNext) {
    //     this.indexForGeneralMaterial++;
    //   } else {
    //     this.indexForGeneralMaterial--;
    //   }
    // }

    hideNavbar(toHide) {
      if (toHide) {
        this.showNavbar = false;
      } else {
        this.showNavbar = true;
      }
    },

    toShowCloudBg(show) {
      this.$emit("to-show-cloud-bg", show);
    },

    finishedMainSubjBox() {
      this.$emit("next-section-to-study");
      this.partToShow = 0;
      this.thePart = 0;
      this.showTheSection = false;
    },
    changeShowWarning(toShow) {
      if(toShow) {
        this.showWarning = true;
      } else {
        this.showWarning = false;
      }
    }
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
