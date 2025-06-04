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
      :isAContinuance="isAContinuance"
      @to-next-board="nextInStartSign"
      @to-prev-board="backToStartSign"
      @back-to-general-material="backToGeneralMaterialFromOperation"
      @to-show-cloud-bg="toShowCloudBg"
      @send-exam-variables="updateExamVariables"
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
      :indexOrder="indexOrderInGenearlMaterial"
      @change-home-icon="ChangeHomeIcon"
      @show-american-ques="showAmericanQues"
      @hide-navbar="hideNavbar"
      @update-color-icon-home="updateColorIconPhone"
      @to-show-cloud-bg="toShowCloudBg"
      @finished-genearal-material="finishedMainSubjBox(0)"
      @update-index-order="updateIndexOrderInGenearlMaterial"
    ></general-material>

    <operation
      v-if="sectionToStudy === 1 && showTheSection && partToShow === 1"
      @update-color-icon-home="updateColorIconPhone"
      @hide-navbar="hideNavbar"
      @back-to-start-sign="backToStartSign"
      :navbarSubjNum="subNavPart"
      @change-sub-nav-num="changeSubNavNum"
      @finished-operation="finishedMainSubjBox(1)"
    ></operation>

    <exam
    :fullName="fullName"
    :idNumber="idNum"
      v-if="sectionToStudy === 2 && showTheSection && partToShow !== 2"
    ></exam>
  </div>
</template>

<script>
import GeneralMaterial from "./GeneralMaterial.vue";
import Navbar from "./Navbar.vue";
import Operation from "./Operation.vue";
import StartSign from "./StartSign.vue";
import Exam from "./Exam.vue";

export default {
  name: "info-screen",
  components: { Navbar, StartSign, GeneralMaterial, Operation, Exam },
  props: ["chosenCourse", "firstChosen", "sectionToStudy"],
  data() {
    return {
      partToShow: 0,
      thePart: 0,
      colorIconPhone: "none",
      Infopart: 1,
      infoHangingPart: 0,
      subNavPart: 1,
      showTheSection: false,
      indexOrderInGenearlMaterial: 0,
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
      showNavbar: true,

      //about start sign
      isAContinuance: false,

      //about exam
      fullName: "",
      idNum: "",
    };
  },
  methods: {
    updateExamVariables(n, i) {
      this.fullName = n;
      this.idNum = i;
    },
    //מראה חלק הבא בקומפוננטת StartSign או שמעביר לחלק של הלמידה שהמשתמש בחר
    nextInStartSign() {
      if (this.thePart === 0) {
        this.thePart++;
      } else {
        if (this.sectionToStudy !== 2) {
          this.updateColorIconPhone(
            "invert(1) brightness(100%) saturate(25%) contrast(100%)"
          );
          this.showNavbar = true;
        } else {
          this.showNavbar = false;
        }
        this.showTheSection = true;
        this.subNavPart = 1;
        this.partToShow++; //shows now the navbar
      }
    },
    //מחזיר לקומפוננטה StartSign או שעושה חזור בקומפוננטה עצמה
    backToStartSign() {
      if (this.showTheSection) {
        this.showTheSection = false;
        this.partToShow--;

        this.thePart = 1;

        this.updateColorIconPhone("none");
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

    finishedMainSubjBox(numBox) {
      if (numBox === 0) {
        this.$emit("next-section-to-study");
        this.partToShow = 0;
        this.thePart = 0;
        this.showTheSection = false;
        this.isAContinuance = true;
      } else {
        this.toHomePage();
        this.$emit("finished-operation");
      }
    },

    backToGeneralMaterialFromOperation() {
      this.$emit("prev-studied-section");
      this.partToShow = 1;
      this.thePart = 1;
      this.subNavPart = 9;
      this.indexOrderInGenearlMaterial = 8;
      this.showTheSection = true;
      this.isAContinuance = false;
    },
    
    updateIndexOrderInGenearlMaterial(isUp) {
      if (isUp) {
        this.indexOrderInGenearlMaterial++;
      } else {
        this.indexOrderInGenearlMaterial--;
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
    left: 4rem;
  }
}
</style>
