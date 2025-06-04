<template>
  <div id="general-material" :style="{ '--moving-btn-color': movingBtnColor }">
    <info-hanging-board
      v-if="
        indexOrder === 0 ||
        (indexOrder === 3 && isInWinches && partInWinches === 0) || indexOrder === 5 || indexOrder === 6
      "
      :sectionHangingBoard="infoHangingBoardPart"
      :chosenCourse="chosenCourse"
      :flipStart="flipStart"
      :flipEndDefine="flipEndDefine"
      :backFlip="backFlip"
      :flipEndSaftyRules="flipEndSaftyRules"
      :flipHook="flipHook"
      @showNextBtnSafetyRules="showNextBtnSafetyRules"
      :inWinches="isInWinches"
    ></info-hanging-board>

    <types-of-cranes
      @crane-card-chosen="CraneCardChosen"
      v-if="indexOrder === 1"
      :cardClicked="craneCardClicked"
      :title="titleTypesCranesIndex"
      :partLearningCraneCard="partLearningCraneCard"
      :arrLearnedCards="arrChosenCardCranes"
      @clicked-question-mark="clickedQuestionMark"
    ></types-of-cranes>

    <american-questions
      v-if="indexOrder === 2"
      @back-to-info="backFromQues"
      @next-part="nextPart"
      @hide-navbar="hideNavbar"
      @update-color-icon-home="updateColorHomeIcon"
    ></american-questions>

    <winches
      v-if="indexOrder === 3"
      @show-tiny-board="showTinyBoard"
      :partInWinches="partInWinches"
      @add-learned-winch-in-sign="addLearnedWinchInArray"
      @show-next-btn="showTheNextBtn"
      :isClickedWinchImg="isInWinches"
      :learnedInWinchSign="learnedInWinchSign"
    ></winches>

    <crane-components v-if="indexOrder === 4" @show-next-btn="showNextBtnFromComponent" :finishLearning="finishLearningComponents" @update-finish-learning="updateFinishLearningComponents"></crane-components>
    <clouds-btns v-if="indexOrder === 7"  @show-next-btn="showNextBtnFromComponent"></clouds-btns>
    <final-highlights  v-if="indexOrder === 8"></final-highlights>


    <p v-if="showNextBtn" class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p v-if="showBackBtn" class="back-btn moving-btn" @click="prevPart">חזור</p>
  </div>
</template>

<script>
import AmericanQuestions from "./AmericanQuestions.vue";
import CloudsBtns from './CloudsBtns.vue';
import CraneComponents from './CraneComponents.vue';
import FinalHighlights from './FinalHighlights.vue';
import InfoHangingBoard from "./InfoHangingBoard.vue";
import TypesOfCranes from "./TypesOfCranes.vue";
import Winches from "./Winches.vue";
export default {
  name: "general-material",

  components: { InfoHangingBoard, TypesOfCranes, AmericanQuestions, Winches, CraneComponents, CloudsBtns, FinalHighlights },
  props: [
    "chosenCourse",
    "navbarSubjNum",
    "colorIconPhone",
     "indexOrder"
  ],
  data() {
    return {
      infoHangingBoardPart: 0,

      //about the flip according to click
      flipStart: false,
      flipEndDefine: false,
      backFlip: false,
      flipEndSaftyRules: false,
      showNextBtn: true,
      seenSafetyRules: false,
      flipHook: true,

      //aboutCarousel
      prevToCarousel: false,
      craneCardClicked: false,
      titleTypesCranesIndex: "סוגי העגורנים הקיימים",
      counterLearnedCranes: 0,
      partLearningCraneCard: 0,
      arrChosenCardCranes: ["", "", ""],
      showBackBtn: true,
      movingBtnColor: "#8cd0ec",
      questionMarkClicked: false,
      //aboutAmericanQues
      finishedAmericanQues: false,
      //about winch componnent
      isInWinches: false,
      partInWinches: 0,
      learnedInWinchSign: [false, false, false, false],
      //about craneComponents
      finishLearningComponents: false,
    };
  },
  methods: {
    nextPart() {
      switch (this.navbarSubjNum) {
        case 1: {
          //checks if user hasnt studied safety rules once
          if (!this.seenSafetyRules) {
            this.showNextBtn = false;
          }
          this.firstFlipInfoHangingBoard();
          this.$emit("change-sub-nav-num", true);

          break;
        }
        case 2: {
          this.$emit('update-index-order', true);
          this.$emit("change-sub-nav-num", true);
          if (this.counterLearnedCranes !== 3) {
            this.showNextBtn = false;
          } else {
            this.showNextBtn = true;
          }
          break;
        }
        case 3: {
          //אם נלחץ קלף ובחלק הראשון של הלמידה- תעביר לשני
          if (this.craneCardClicked && this.partLearningCraneCard === 0) {
            this.partLearningCraneCard++;
            if (
              this.titleTypesCranesIndex === "עגורן שער" &&
              !this.questionMarkClicked
            ) {
              this.showNextBtn = false;
            }
          } else if (
            //אם נלחץ קלף אבל אנחנו בחלק השני והאחרון של הקלף ללמידה- אז להחזיר קרוסלת הקלפים
            this.craneCardClicked &&
            this.partLearningCraneCard === 1
          ) {
            this.craneCardClicked = false;
            //אם הקלף שנלמד לפני רגע, נלמד פעם ראשונה
            //הכנסה של קלף העגורן למערך של אלו שנלמדו במידה ולא נלמד כבר
            if (!this.checkIfLearnedCard(this.titleTypesCranesIndex)) {
              this.counterLearnedCranes++;
              this.arrChosenCardCranes[this.counterLearnedCranes] =
                this.titleTypesCranesIndex;
            }
            //מחזירה למאפיינים שהיו לפני שנלחץ כרטיס
            this.movingBtnColor = "#8cd0ec";
            this.titleTypesCranesIndex = "סוגי העגורנים הקיימים";
            this.prevToCarousel = false;
            this.partLearningCraneCard = 0; //מאפס את החלק שלומדים בלחיצה על קלף
            if (this.counterLearnedCranes !== 3) {
              this.showNextBtn = false;
            } else {
              this.showNextBtn = true;
            }
          } else {
            //במידה וסיימו את כל הקלפים ולוחצים הבא לנושא החדש
            this.$emit("change-sub-nav-num", true);
            this.hideNavbar(true);
            this.$emit('update-index-order', true);
            if(!this.finishedAmericanQues) {
              this.showNextBtn = false;
            } else {
              this.showNextBtn = true;
            }
            this.showBackBtn = false;
          }
          break;
        }
        case 4: {
          //if next from questions
          if (this.indexOrder === 2) {
            this.$emit('update-index-order', true);
            this.hideNavbar(false);
            this.showBackBtn = true;
            //check if was already in this page
            if (!this.isInWinches) {
              this.showNextBtn = false;
            }
          } else if (this.partInWinches === 0) {
            this.partInWinches++;
            if (this.checksIfLearnedAllBtns()) {
              this.showNextBtn = true;
            } else {
              this.showNextBtn = false;
            }
          } else if (this.partInWinches === 1) {
            this.$emit('update-index-order', true);
            this.$emit("change-sub-nav-num", true);
            if(!this.finishLearningComponents) {
              this.showNextBtn = false;
            }
          }
          break;
        }
        case 5 : {
          this.$emit("change-sub-nav-num", true);
          this.$emit('update-index-order', true);
          //to show the right part in infoHangingBoard
          this.flipEndSaftyRules = true;
        this.flipStart = false;
        this.flipHook = true;
          this.infoHangingBoardPart++;
          this.isInWinches = false;
          break;
        }
        case 6 : {
          this.$emit("change-sub-nav-num", true);
          this.$emit('update-index-order', true);
          //to show the right part in infoHangingBoard
          
          this.firstFlipInfoHangingBoard();
          break;
        }
        case 7 : {
          this.$emit("change-sub-nav-num", true);
          this.$emit('update-index-order', true);
          this.showNextBtn = false;
          this.toShowCloudBg(false);
          break;
        }
        case 8 : {
          this.toShowCloudBg(true);
          this.$emit('update-index-order', true);
          this.$emit("change-sub-nav-num", true);
          this.showNextBtn = true;
          this.hideNavbar(true);

          break;
        }
        case 9 : {
          this.$emit('finished-genearal-material');
        }
      }
    },
    prevPart() {
      switch (this.navbarSubjNum) {
        case 1: {
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
          if (this.craneCardClicked && this.partLearningCraneCard === 0) {
            this.craneCardClicked = false;
            this.titleTypesCranesIndex = "סוגי העגורנים הקיימים";
            this.prevToCarousel = false;
            if (this.counterLearnedCranes !== 3) {
              this.showNextBtn = false;
            } else {
              this.showNextBtn = true;
            }
          } else if (
            this.craneCardClicked &&
            this.partLearningCraneCard === 1
          ) {
            this.partLearningCraneCard--;
          } else {
            this.$emit("change-sub-nav-num", false);
            this.$emit('update-index-order', false);
            this.showNextBtn = true;

          }
          break;
        }
        case 4: {
          //back to ques
          if (this.partInWinches === 0) {
            this.$emit('update-index-order', false);
            this.hideNavbar(true);
            this.showBackBtn = false;
            this.showNextBtn = true;
            this.finishedAmericanQues = true;
            this.isInWinches = false;
          } else {
            this.partInWinches--;
            this.showNextBtn = true;
          }
          break;
        }
        case 5: {
          this.$emit('update-index-order', false);
          this.$emit("change-sub-nav-num", false);
          this.showNextBtn = true;
          break;
        }
        case 6: {
          this.$emit("change-sub-nav-num", false);
          this.$emit('update-index-order', false);
          //to show the right part in infoHangingBoard 
          this.infoHangingBoardPart--;
          this.isInWinches = true;
          break;
        }
        case 7 : {
          this.$emit("change-sub-nav-num", false);
          this.$emit('update-index-order', false);
          //to show the right part in infoHangingBoard
           this.reversedFlipInfoHangingBoard();
          break;
        }
        case 8 : {
          this.$emit("change-sub-nav-num", false);
          this.$emit('update-index-order', false);
          this.showNextBtn = true;
          this.toShowCloudBg(true);
          //if was already in the operation part and got here from the prev btn
          this.infoHangingBoardPart = 3;
          break;
        }
        case 9: {
          this.$emit("change-sub-nav-num", false);
          this.$emit('update-index-order', false);
          this.toShowCloudBg(false);
          this.hideNavbar(false);
          this.showNextBtn = true;

        }
      }
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
      this.backFlip = true;
      let timer = setTimeout(() => {
        this.infoHangingBoardPart--;
        //to restart value
        this.flipEndSaftyRules = true;
        this.flipStart = false;
        this.flipHook = true;
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
      this.showNextBtn = true;
      //color moving btns
      switch (craneTitle) {
        case "עגורן גשר":
          return (this.movingBtnColor = "#C8A47C");
        case "עגורן שער":
          return (this.movingBtnColor = "#6F97BA");
        case "עגורן עמוד":
          return (this.movingBtnColor = "#BADDF4");
      }
    },

    //בודקת אם הקלף של העגורן נלמד כבר
    checkIfLearnedCard(craneTitle) {
      for (let i = 0; i < this.arrChosenCardCranes.length; i++) {
        if (this.arrChosenCardCranes[i] === craneTitle) {
          return true;
        }
      }
      return false;
    },

    backFromQues() {
      this.$emit("change-sub-nav-num", false);
      this.$emit('update-index-order', false);
      this.showNextBtn = true;
      this.showBackBtn = true;
    },

    clickedQuestionMark() {
      this.questionMarkClicked = true;
      this.showNextBtn = true;
    },

    hideNavbar(tohide) {
      if (tohide) {
        this.$emit("hide-navbar", true);
        this.updateColorHomeIcon(
              "none"
            );
      } else {
        this.$emit("hide-navbar", false);
        this.updateColorHomeIcon(
              "invert(1) brightness(100%) saturate(25%) contrast(100%)"
            );
      }
    },

    updateColorHomeIcon(color) {
      this.$emit("update-color-icon-home", color);
    },
    //about winch componnent
    showTinyBoard() {
      this.isInWinches = true;
      this.showNextBtn = true;
    },

    addLearnedWinchInArray(index) {
      this.learnedInWinchSign[index] = true;
      if (this.checksIfLearnedAllBtns()) {
        this.showNextBtn = true;
      }
    },
    checksIfLearnedAllBtns() {
      for (let i = 0; i < this.learnedInWinchSign.length; i++) {
        if (!this.learnedInWinchSign[i]) {
          return false;
        }
      }
      return true;
    },
    showNextBtnFromComponent() {
      this.showNextBtn  = true;
    },

    updateFinishLearningComponents(isFinished) {
      this.finishLearningComponents = isFinished;
    },

    toShowCloudBg(show) {
      this.$emit('to-show-cloud-bg', show);
    },
  },
};
</script>

<style scoped>
#general-material {
  z-index: 1;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.moving-btn {
  z-index: 1;
  position: absolute;
  bottom: 1rem;
  width: 5rem;
  height: 3rem;
  font-size: 1rem;
  background-color: var(--moving-btn-color);
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
