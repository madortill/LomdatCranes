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
      :partNum="sectionToStudy"
      :firstChosen="firstChosen"
      :thePart="indexOrder"
      v-if="indexOrder < 2"
    ></start-sign>
    <navbar
      :part="navPart"
      :subjNum="subNavPart"
      v-if="indexOrder > 1"
    ></navbar>
    <div class="fix-layer" v-if="sectionToStudy === 0">
      <info-hanging-board
        v-if="indexOrder === 2"
        :section="infoHangingPart"
        :chosenCourse="chosenCourse"
        :flipStart="flipStart"
        :flipEndDefine="flipEndDefine"
        :backFlip="backFlip"
        :flipEndSaftyRules="flipEndSaftyRules"
        @showNextBtnSafetyRules="showNextBtnSafetyRules"
      ></info-hanging-board>

      <types-of-cranes
        @crane-card-chosen="CraneCardChosen"
        v-if="indexOrder === 3"
        :cardClicked="craneCardClicked"
        :title="titleTypesCranesIndex"
      ></types-of-cranes>
    </div>

    <p v-if="showNextBtn" class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p v-if="indexOrder > 0" class="back-btn moving-btn" @click="prevPart">
      חזור
    </p>
  </div>
</template>

<script>
import CraneCard from "./CraneCard.vue";
import InfoHangingBoard from "./InfoHangingBoard.vue";
import Navbar from "./Navbar.vue";
import StartSign from "./StartSign.vue";
import TypesOfCranes from "./TypesOfCranes.vue";
export default {
  name: "info-screen",
  components: { Navbar, InfoHangingBoard, StartSign, TypesOfCranes },
  props: [
    "navPart",
    "chosenCourse",
    "firstChosen",
    "sectionToStudy",
    "colorIconPhone",
  ],
  data() {
    return {
      showSelection: false,
      indexOrder: 0,
      Infopart: 1,
      infoHangingPart: 0,
      subNavPart: 1,
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
      if (this.sectionToStudy === 0) {
        //if in the first screen of the startSign
        if (this.indexOrder === 2 && this.infoHangingPart === 0) {
          this.subNavPart++;
          //checks if user hasnt studied safety rules once
          if (!this.seenSafetyRules) {
            this.showNextBtn = false;
          }
          this.firstFlipInfoHangingBoard();
        } else {
          this.indexOrder++; //shows next info
          if (this.indexOrder > 2) {
            this.subNavPart++;
            if (this.indexOrder === 3) {
              this.showNextBtn = false;
            }
          } else if (this.indexOrder === 2) {
            this.$emit(
              "updateColorIconPhone",
              "invert(1) brightness(100%) saturate(25%) contrast(100%)"
            );
          }
        }
      }
    },
    prevPart() {
      //if chose the start of the lomda
      if (this.sectionToStudy === 0) {
        //if in the second screen of the startSign
        if (this.infoHangingPart === 1 && this.indexOrder === 2) {
          this.subNavPart--;
          this.secondFlipInfoHangingBoard();
        }
        //in case from a chosen card in the crane carousel
      else if (this.prevToCarousel) {
        this.craneCardClicked = false;
        this.titleTypesCranesIndex = "סוגי העגורנים הקיימים";
        this.prevToCarousel = false;
      } else {
        this.indexOrder--;
        if (this.indexOrder < 2) {
          this.$emit("updateColorIconPhone", "none");
        } else {
          this.subNavPart--;
        }
      }
      this.showNextBtn = true; //לבדוק על זה שעושים חזור
      }

      
    },

    firstFlipInfoHangingBoard() {
      //to restart value
      this.flipEndSaftyRules = false;
      this.backFlip = false;
      //the flip animation
      this.flipEndDefine = true;
      let timer = setTimeout(() => {
        this.infoHangingPart++;
        this.flipStart = true;
        clearTimeout(timer);
      }, 590);
    },
    secondFlipInfoHangingBoard() {
      //to restart values
      this.flipEndDefine = false;
      this.flipStart = false;
      //
      this.backFlip = true;
      let timer = setTimeout(() => {
        this.infoHangingPart--;
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
#info-screen {
  z-index: 7;
  width: 100vw;
  height: 100vh;
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
.fix-layer {
  z-index: 1;
}

@media screen and (max-width: 600px) {
  .homeIcon {
    filter: var(--home-icon-color);
    right: auto;
    left: 4.6rem;
  }
}
</style>
