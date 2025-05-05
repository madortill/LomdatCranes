<template>
  <div id="operation" :style="{ '--moving-btn-color': movingBtnColor }">
    <div class="hide-down-instruction"></div>
    <instruction class="down" :numInstruction="numInstruction"></instruction>
    <electric-panel></electric-panel>
     <!-- <img src="/media/Operation/electricPanel.svg"/> -->
    <p v-if="showNextBtn" class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p v-if="showBackBtn" class="back-btn moving-btn" @click="prevPart">חזור</p>
  </div>
</template>

<script>
import ElectricPanel from './ElectricPanel.vue';
import Instruction from './Instruction.vue';
export default {
  name: "operation",

  components: {Instruction, ElectricPanel},
  props: ["chosenCourse", "navbarSubjNum", "colorIconPhone"],
  data() {
    return {
      indexOrder: 0,
      showNextBtn: true,
      showBackBtn: true,
      numInstruction: 0,
    };
  },
  methods: {
    nextPart() {
      switch (this.navbarSubjNum) {
        case 1: {


          break;
        }
        case 2: {
          // this.indexOrder++;
          // this.$emit("change-sub-nav-num", true);
          // if (this.counterLearnedCranes !== 3) {
          //   this.showNextBtn = false;
          // } else {
          //   this.showNextBtn = true;
          // }
          break;
        }
        case 3: {
          break;
        }
      }
    },
    prevPart() {
      switch (this.navbarSubjNum) {
        case 1: {
          // if (this.infoHangingBoardPart === 0) {
          this.$emit("back-to-start-sign");

          break;
        }
        case 2: {
          // this.$emit("change-sub-nav-num", false);
          // this.reversedFlipInfoHangingBoard();
          // this.showNextBtn = true;
          break;
        }
      }
    },

    toHomePage() {
      this.$emit("toHomePage");
    },

    // hideNavbar(tohide) {
    //   if (tohide) {
    //     this.$emit("hide-navbar", true);
    //   } else {
    //     this.$emit("hide-navbar", false);
    //   }
    // },

    // updateColorHomeIcon(color) {
    //   this.$emit("update-color-icon-home", color);
    // },

    // showNextBtnFromComponent() {
    //   this.showNextBtn = true;
    // },

    // toShowCloudBg(show) {
    //   this.$emit("to-show-cloud-bg", show);
    // },
    
  },
//   mounted() {
//     setTimeout(() => {
        
//     }, 1000);
//   },
};
</script>

<style scoped>
#operation {
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

.hide-down-instruction {
    background-color: #e0f2f4;
    height: 3rem;
    width: 10rem;
    z-index: 2;
}

.down {
    z-index: 0;
  animation: goingDown 0.6s linear forwards;
}

@keyframes goingDown {
  0% {
    position: relative;
    bottom: 10vh;
  }
  100% {
    position: relative;
    bottom: 0vh;
  }
}
</style>
