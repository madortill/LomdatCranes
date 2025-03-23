<template>
  <div id="info-screen">
    <img
      @click="toHomePage"
      class="homeIcon"
      :style="{ '--home-icon-color': colorIconPhone}"
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
      ></info-hanging-board>
    </div>

    <p class="next-btn moving-btn" @click="nextPart">הבא</p>
    <p v-if="indexOrder > 0" class="back-btn moving-btn" @click="prevPart">
      חזור
    </p>
  </div>
</template>

<script>
import InfoHangingBoard from "./InfoHangingBoard.vue";
import Navbar from "./Navbar.vue";
import StartSign from "./StartSign.vue";
export default {
  name: "info-screen",
  components: { Navbar, InfoHangingBoard, StartSign },
  props: ["navPart", "chosenCourse", "firstChosen", "sectionToStudy", "colorIconPhone"],
  data() {
    return {
      // part: 0,
      // partNum: 0,
      // firstChosen: null,
      showSelection: false,
      // colorIconPhone: 'none',
      indexOrder: 0,
      Infopart: 1,
      infoHangingPart: 0,
      subNavPart: 1,
      flipStart: false,
      flipEndDefine: false,
      backFlip: false,
      flipEndSaftyRules: false,
    };
  },
  methods: {
    nextPart() {
      if (this.indexOrder === 2 && this.infoHangingPart === 0) {
        //to restart values
        this.flipEndSaftyRules = false;
        this.backFlip = false;
        //
        this.subNavPart++;
        this.flipEndDefine = true;
        let timer = setTimeout(() => {
          this.infoHangingPart++;
          this.flipStart = true;
          clearTimeout(timer);
        }, 590);
      } else {
        this.indexOrder++;
        if (this.indexOrder === 2) {
          this.$emit('updateColorIconPhone', 'invert(1) brightness(100%) saturate(25%) contrast(100%)');
        }
      }
    },
    prevPart() {
      if (this.infoHangingPart === 1) {
        //to restart values
        this.flipEndDefine = false;
        this.flipStart = false;
        //
        this.subNavPart--;
        this.backFlip = true;
        let timer = setTimeout(() => {
          this.infoHangingPart--;
          this.flipEndSaftyRules = true;
          clearTimeout(timer);
        }, 590);
      } else {
        this.indexOrder--;
        if(this.indexOrder < 2) {
          this.$emit('updateColorIconPhone', 'none');
        }
      }
    },
    toHomePage () {
      this.$emit('toHomePage');
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
