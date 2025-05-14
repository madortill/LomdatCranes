<template>
  <div id="operation" :style="{ '--moving-btn-color': movingBtnColor }">
    <div class="hide-down-instruction"></div>
    <instruction
      v-if="partInSecondPart === -1"
      class="down"
      :numInstruction="numInstruction"
    ></instruction>

    <div
      v-if="partInSecondPart === -1"
      class="graphics-container"
      :class="partInRemote === 3 ? 'fix-flex-dir' : ''"
    >
      <!-- <div> -->
      <electric-panel
        @next-instruction="nextPart"
        :numPart="partInElectricPanel"
        :class="[
          numInstruction > 1 ? 'disabled-remote' : '',
          numInstruction < 5 ? '' : 'hide',
        ]"
      />
      <!-- </div> -->

      <div class="remote-container">
        <remote
          @next-instruction="nextPart"
          :numPart="partInRemote"
          :isAble="navbarSubjNum === 2 ? true : false"
          :isZoomInRemote="false"
          :class="[numInstruction < 2 ? 'disabled-remote' : '']"
        />
        <remote
          @next-instruction="nextPart"
          :class="numInstruction < 4 ? 'hide' : ''"
          :isZoomInRemote="true"
          :numPart="partInRemote"
        />
      </div>
      <div class="crane-in-operation-container">
        <crane-in-operation :class="numInstruction < 5 ? 'hide' : ''" />
      </div>
    </div>

    <summary-operation v-if="partInSecondPart > -1"/>

    <p v-if="showNextBtn" class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p v-if="showBackBtn" class="back-btn moving-btn" @click="prevPart">חזור</p>
  </div>
</template>

<script>
import ElectricPanel from "./ElectricPanel.vue";
import Instruction from "./Instruction.vue";
import CraneInOperation from "./CraneInOperation.vue";
import Remote from "./Remote.vue";
import SummaryOperation from './SummaryOperation.vue';
export default {
  name: "operation",

  components: { Instruction, ElectricPanel, Remote, CraneInOperation, SummaryOperation },
  props: ["navbarSubjNum", "colorIconPhone"],
  data() {
    return {
      showNextBtn: false,
      showBackBtn: true,
      numInstruction: 0,
      partInElectricPanel: 0,
      partInRemote: 0,
      isZoomInRemote: false,
      partInSecondPart: -1,
    };
  },
  methods: {
    nextPart() {
      switch (this.navbarSubjNum) {
        case 1: {
          this.partInElectricPanel++;
          this.numInstruction++;
          if (this.numInstruction === 2) {
            this.$emit("change-sub-nav-num", true);
          }
          break;
        }
        case 2: {
          this.partInRemote++;
          this.numInstruction++;
          if (this.numInstruction === 1 || this.numInstruction === 4) {
            this.$emit("change-sub-nav-num", true);
          }
          break;
        }
        case 3: {
          this.partInRemote++;
          this.numInstruction++;
          this.$emit("change-sub-nav-num", true);
          //temparery
          this.showNextBtn = true;
          break;
        }
        case 4: {
          if (this.partInSecondPart === -1) {
            this.hideNavbar(true);
          }
          this.partInSecondPart++;
          break;
        }
      }
    },
    prevPart() {
      switch (this.navbarSubjNum) {
        case 1: {
          if (this.partInElectricPanel === 0) {
            this.$emit("back-to-start-sign");
          } else {
            this.numInstruction--;
            this.partInElectricPanel--;
          }
          break;
        }
        case 2: {
          if (this.partInRemote === 0) {
            this.partInElectricPanel--;
            this.$emit("change-sub-nav-num", false);
          } else {
            this.partInRemote--;
          }
          this.numInstruction--;
          break;
        }
        case 3: {
          this.$emit("change-sub-nav-num", false);
          this.partInRemote--;
          this.numInstruction--;
          break;
        }
        case 4: {
          if (this.partInSecondPart === -1) {
            this.$emit("change-sub-nav-num", false);
            this.partInRemote--;
            this.numInstruction--;
            //temparery
             this.showNextBtn = false;
          } else {
            if (this.partInSecondPart === 0) {
            this.hideNavbar(false);
          }
            this.partInSecondPart--;
          }

          break;
        }
      }
    },

    toHomePage() {
      this.$emit("toHomePage");
    },

    hideNavbar(tohide) {
      if (tohide) {
        this.$emit("hide-navbar", true);
      } else {
        this.$emit("hide-navbar", false);
      }
    },

    // updateColorHomeIcon(color) {
    //   this.$emit("update-color-icon-home", color);
    // },

    // showNextBtn() {

    // },

    // toShowCloudBg(show) {
    //   this.$emit("to-show-cloud-bg", show);
    // },
  },
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
  justify-content: space-between;
}

.steps-container {
  width: 100vw;
  height: 100vh;
}
.crane-in-operation-container {
  background-color: gray;
  border-radius: 1rem;
}
.graphics-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 80%;
}

.disabled-remote {
  filter: grayscale(100%);
}

.hide {
  display: none;
}

.remote-container {
  display: flex;
  height: 100%;
  align-items: center;
  /* position: relative; */
  width: 20rem;
  justify-content: center;
}

/* .remote {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  display: none; 
} */

.moving-btn {
  z-index: 5;
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
  width: 100%;
  z-index: 4;
  position: absolute;
  top: 0rem;
  left: 50%;
  transform: translateX(-50%);
}

.down {
  z-index: 3;
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

@media screen and (max-width: 600px) {
  #operation {
    height: 91vh;
  }

  .graphics-container {
    /* align-items: flex-end; */
    flex-direction: column-reverse;
    /* margin-bottom: 6.5rem; */
  }
  .fix-flex-dir {
    flex-direction: column;
  }
}
</style>
