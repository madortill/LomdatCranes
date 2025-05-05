<template>
  <div id="operation" :style="{ '--moving-btn-color': movingBtnColor }">
    <p v-if="showNextBtn" class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p v-if="showBackBtn" class="back-btn moving-btn" @click="prevPart">חזור</p>
  </div>
</template>

<script>
export default {
  name: "operation",

  components: {},
  props: ["chosenCourse", "navbarSubjNum", "colorIconPhone"],
  data() {
    return {
      indexOrder: 0,
      showNextBtn: true,
      showBackBtn: true,
    };
  },
  methods: {
    nextPart() {
      switch (this.navbarSubjNum) {
        case 1: {
          // if (this.infoHangingBoardPart === 0) {
          //checks if user hasnt studied safety rules once
          // if (!this.seenSafetyRules) {
          //   this.showNextBtn = false;
          // }
          // this.firstFlipInfoHangingBoard();
          // // }
          // this.$emit("change-sub-nav-num", true);

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

    hideNavbar(tohide) {
      if (tohide) {
        this.$emit("hide-navbar", true);
      } else {
        this.$emit("hide-navbar", false);
      }
    },

    updateColorHomeIcon(color) {
      this.$emit("update-color-icon-home", color);
    },

    showNextBtnFromComponent() {
      this.showNextBtn = true;
    },

    toShowCloudBg(show) {
      this.$emit("to-show-cloud-bg", show);
    },
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
</style>
