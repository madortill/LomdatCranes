<template>
  <div id="open-page">
    <button @click="showInfo" class="info-btn btn">i</button>
    <img class="tillLogo" src="/media/whiteMadorTill.png" alt="tillLogo" />
    <lomda-info @hide-info="hideInfo" v-if="isOpenInfo"></lomda-info>
    <div class="start-container" v-if="!isOpenInfo">
      <img src="/media/Crane.png" alt="crane" class="bgCrane" />

      <start-hanging-board
        @toNextBoard="toNextScreen"
        :indexYellowSign="indexYellowSign"
        :showSelection="showSelection"
        :partNum="boardNum"
        :craneKind="chosenCrane"
        :isUp="isUp"
        :isDown="isDown"
      />

      <div class="box-container" v-if="boardNum === 1 && !showSelection">
        <Box
          @click.once="toNextScreen"
          id="עילי"
          class="box btn"
          :class="{ fadeObject: chosenCrane !== '' }"
          newTitle="עילי"
          partBox="0"
        ></Box>
        <Box
          id="disable"
          class="box btn"
          :class="{ fadeObject: chosenCrane !== '' }"
          newTitle="disable"
          partBox="-1"
        ></Box>
        <!-- <Box @click.once="toNextScreen" id="העמסה עצמית" class="box btn" :class="{fadeObject: chosenCrane !== ''}" newTitle="העמסה עצמית"></Box>  -->
      </div>

      <div class="home-box-container" v-if="boardNum === 3 || showSelection">
        <Box
          @click="toStudy(0)"
          class="part-one btn"
          newTitle="תחילת הלמידה"
          partBox="1"
          id=""
        ></Box>
        <Box
          @click="toStudy(1)"
          class="part-two btn"
          newTitle="תפעול"
          partBox="1"
        ></Box>
        <Box
          @click="toStudy(2)"
          class="part-three btn"
          newTitle="מבחן"
          partBox="1"
        ></Box>
      </div>
    </div>
    <div class="ground"></div>
  </div>
</template>

<script>
import Box from "../../src/components/Box.vue";
import LomdaInfo from './lomdaInfo.vue';
import StartHangingBoard from "./StartHangingBoard.vue";

export default {
  name: "open-page",
  components: { Box, StartHangingBoard, LomdaInfo },
  props: ["showSelection", "indexYellowSign"],
  data() {
    return {
      // infoObject: {
      //   "מפתחת לומדה ראשית:": 'רב"ט דני שריקי',
      //   "גרפיקאית:": 'רב"ט קריסטינה ברחטוב, רב"ט דני שריקי',
      //   "מומחה תוכן:": 'רס"ר יוחאי עזרא',
      //   'רמ"ד טי"ל:': 'רס"מ שלומי אוגרן',
      //   "גרסה:": "ינואר 2025",
      // },
      isOpenInfo: false,
      chosenCrane: "",
      showExplain: false,
      boardNum: 1,
      isUp: false,
      isDown: false,
      fChosen: true,
    };
  },
  methods: {
    showInfo() {
      this.isOpenInfo = true;
    },
    hideInfo() {
      this.isOpenInfo = false;
    },
    toNextScreen(event) {
      if (this.boardNum === 1) {
        this.chosenCrane = event.currentTarget.id;
        this.$emit("theChosenCourse", this.chosenCrane);
        this.$emit("next-index-yellow-sign");
      }
      this.isUp = true;
      let timerdown = setTimeout(() => {
        this.isDown = true;
        this.boardNum++;
        clearTimeout(timerdown);
      }, 800);
      let timer = setTimeout(() => {
        this.isUp = false;
        this.isDown = false;
        clearTimeout(timer);
      }, 1500);
    },
    toStudy(part) {
      this.$emit("to-study", this.fChosen, part);
      if (this.fChosen) {
        this.fChosen = true;
      }
    },
  },
};
</script>

<style scoped>
#open-page {
  direction: rtl;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100vw;
  flex-direction: column;
  color: #023047;
}

.btn {
  cursor: pointer;
  pointer-events: visiblePainted;
}

.box {
  z-index: 1;
  position: relative;
}

.disabled {
  height: 90%;
  padding-bottom: 1rem;
}

.box-container {
  width: 100vw;
  height: 50vh;
  display: flex;
  z-index: 1;
  justify-content: space-evenly;
  align-items: center;
}

.home-box-container {
  width: 20rem;
  height: 80rem;
  display: flex;
  z-index: 1;
  position: relative;
  align-items: center;
  flex-direction: column;
  animation: fadeIn 0.2s linear forwards;
  margin-bottom: 1rem;
  justify-content: center;
}

.part-one {
  position: relative;
  z-index: 4;
  margin-left: 2rem;
}

.part-two {
  position: relative;
  z-index: 3;
  margin-top: -4rem;
  margin-left: -3rem;
}

.part-three {
  position: relative;
  z-index: 2;
  margin-top: -4rem;
}

.info-btn {
  border: 3px solid #ffb703;
  background-color: #ffb703;
  color: #e0f2f4;
  border-radius: 100%;
  width: 2rem;
  height: 2rem;
  padding: 0.2rem;
  font-size: 1rem;
  position: absolute;
  left: 6rem;
  top: 1rem;
  font-weight: bold;
  z-index: 2;
}

.info-btn:hover {
  animation: changeColor 0.2s linear forwards;
}

@keyframes changeColor {
  0% {
    border: 3px solid #ffb703;
    background-color: #ffb703;
  }
  100% {
    background-color: #023047;
    border: 3px solid #023047;
  }
}

.tillLogo {
  position: absolute;
  right: 1rem;
  bottom: 1rem;
  width: 4rem;
  z-index: 2;
}

.bgCrane {
  position: absolute;
  right: -11rem;
  width: 38rem;
  height: 100vh;
  pointer-events: none;
  z-index: 0;
}

.start-container {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-between;
}

.ground {
  background-color: #023047;
  position: absolute;
  bottom: 0rem;
  width: 100vw;
  height: 9rem;
}

@media screen and (max-width: 700px) {
  .ground {
    height: 15rem;
  }

  .box {
    width: 20rem;
    z-index: 1;
    margin-bottom: 0rem;
  }
  .box-container {
    margin-bottom: 5rem;
  }
}

.fadeObject {
  animation: fadeOut 0.2s linear forwards;
}

@keyframes fadeOut {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    visibility: hidden;
  }
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
