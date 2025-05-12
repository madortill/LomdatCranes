<template>
  <div id="operation" :style="{ '--moving-btn-color': movingBtnColor }">
    <div class="hide-down-instruction"></div>
    <instruction class="down" :numInstruction="numInstruction"></instruction>

    <div class="graphics-container">
      <!-- <div> -->
      <electric-panel
        @next-instruction="nextPart"
        :numPart="partInElectricPanel"
        :class="numInstruction > 1 ? 'disabled-remote' : ''"
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
    </div>

    <p v-if="showNextBtn" class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p v-if="showBackBtn" class="back-btn moving-btn" @click="prevPart">חזור</p>
  </div>
</template>

<script>
import ElectricPanel from "./ElectricPanel.vue";
import Instruction from "./Instruction.vue";
import Remote from "./Remote.vue";
export default {
  name: "operation",

  components: { Instruction, ElectricPanel, Remote },
  props: ["chosenCourse", "navbarSubjNum", "colorIconPhone"],
  data() {
    return {
      indexOrder: 0,
      showNextBtn: false,
      showBackBtn: true,
      numInstruction: 0,
      partInElectricPanel: 0,
      partInRemote: 0,
      isZoomInRemote: false,
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
          this.$emit("change-sub-nav-num", false);

          this.partInRemote--;

          this.numInstruction--;

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
  justify-content: space-between;
}

.graphics-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 100vw;
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

@media screen and (max-width: 700px) {
  #operation {
    height: 91vh;
  }

  .graphics-container {
    /* align-items: flex-end; */
    flex-direction: column-reverse;
    /* margin-bottom: 6.5rem; */
  }
}
</style>
