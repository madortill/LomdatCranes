<template>
  <div id="general-material">
    <info-hanging-board
      v-if="indexOrder === 0"
      :sectionHangingBoard="infoHangingBoardPart"
      :chosenCourse="chosenCourse"
      :flipStart="flipStart"
      :flipEndDefine="flipEndDefine"
      :backFlip="backFlip"
      :flipEndSaftyRules="flipEndSaftyRules"
      @showNextBtnSafetyRules="showNextBtnSafetyRules"
    ></info-hanging-board>

    <types-of-cranes
      @crane-card-chosen="CraneCardChosen"
      v-if="indexOrder === 1"
      :cardClicked="craneCardClicked"
      :title="titleTypesCranesIndex"
    ></types-of-cranes>

    <p v-if="showNextBtn" class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p class="back-btn moving-btn" @click="prevPart">חזור</p>
  </div>
</template>

<script>
import InfoHangingBoard from "./InfoHangingBoard.vue";
import TypesOfCranes from "./TypesOfCranes.vue";
export default {
  name: "general-material",

  components: { InfoHangingBoard, TypesOfCranes },
  props: [
    "chosenCourse",
    "navbarSubjNum",
    // "sectionToStudy",
    // "colorIconPhone",
  ],
  data() {
    return {
      indexOrder: 0,
      // Infopart: 1,
      infoHangingBoardPart: 0,
      // subNavPart: 1,
      // showTheSection: false,

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
    nextPart() {
      switch (this.navbarSubjNum) {
        case 1: {
          // if (this.infoHangingBoardPart === 0) {
          //checks if user hasnt studied safety rules once
          if (!this.seenSafetyRules) {
            this.showNextBtn = false;
          }
          this.firstFlipInfoHangingBoard();
          // }
          this.$emit("change-sub-nav-num", true);

          break;
        }
        case 2: {
          this.indexOrder++;
          this.$emit("change-sub-nav-num", true);
          this.showNextBtn = false;
          break;
        }
      }

      //if in the first screen of the startSign
      // if (this.indexOrder === 2 && this.infoHangingPart === 0) {
      // } else {
      //   this.indexOrder++; //shows next info
      //   if (this.indexOrder > 2) {
      //     this.subNavPart++;
      //     if (this.indexOrder === 3) {
      //       this.showNextBtn = false;
      //     }
      //   } else if (this.indexOrder === 2) {
      //     this.$emit(
      //       "updateColorIconPhone",
      //       "invert(1) brightness(100%) saturate(25%) contrast(100%)"
      //     );
      //   }
      // }
    },
    prevPart() {
      switch (this.navbarSubjNum) {
        case 1: {
          // if (this.infoHangingBoardPart === 0) {
          this.$emit("back-to-start-sign");

          break;
        }
        case 2: {
          this.$emit("change-sub-nav-num", false);
          this.reversedFlipInfoHangingBoard();
          this.showNextBtn = true;

          break;
        }
        case 3: {
          if (this.craneCardClicked) {
            this.craneCardClicked = false;
            this.titleTypesCranesIndex = "סוגי העגורנים הקיימים";
            this.prevToCarousel = false;
          } else {
            this.$emit("change-sub-nav-num", false);
            this.indexOrder--;
            this.showNextBtn = true;
          }

          break;
        }
      }

      //in case from a chosen card in the crane carousel
      // if (this.prevToCarousel) {
      //   this.craneCardClicked = false;
      //   this.titleTypesCranesIndex = "סוגי העגורנים הקיימים";
      //   this.prevToCarousel = false;
      // } else {
      //   this.indexOrder--;
      //   if (this.indexOrder < 2) {
      //     this.$emit("updateColorIconPhone", "none");
      //   } else {
      //     this.navbarSubjNum--;
      //   }
      // }
      // this.showNextBtn = true; //לבדוק על זה שעושים חזור
    },

    firstFlipInfoHangingBoard() {
      //to restart value
      this.flipEndSaftyRules = false;
      this.backFlip = false;
      //the flip animation
      this.flipEndDefine = true;
      let timer = setTimeout(() => {
        this.infoHangingBoardPart++;
        this.flipStart = true;
        clearTimeout(timer);
      }, 590);
    },
    reversedFlipInfoHangingBoard() {
      //to restart values
      this.flipEndDefine = false;
      this.flipStart = false;
      //
      this.backFlip = true;
      let timer = setTimeout(() => {
        this.infoHangingBoardPart--;
        this.flipEndSaftyRules = true;
        clearTimeout(timer);
      }, 590);
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
  },
};
</script>

<style scoped>
#general-material {
  z-index: 1;
  width: 80vw;
  /* height: 100vh; */
  display: flex;
  align-items: center;
  flex-direction: column;
}

.moving-btn {
  /* z-index: 1; */
  position: absolute;
  bottom: 1rem;
  width: 5rem;
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
}

.moving-btn:hover {
  background-color: #023047;
  color: white;
}

.next-btn {
  left: 1rem;
}

.back-btn {
  right: 1rem;
}
</style>
