<template>
  <div
    id="info-hanging-board"
    :class="{
      'flip-start-safty-rules': flipStart,
      'flip-end-definition': flipEndDefine,
      'unfliped-board': !flipStart,
      'flip-end-safty-rules': backFlip,
      'flip-start-definition': flipEndSaftyRules,
    }"
  >
    <!-- <img class="board" src="/media/infoHangingBoard.png" alt="infoHangingBoard"/> -->
    <div class="info-container">
      <p class="header">{{ theInfo[section][0] }}</p>
      <p
        v-for="(text, index) in theInfo[section].slice(1)"
        :key="index"
        class="text"
      >
        {{ text }}
      </p>
    </div>
    <img
      class="notice-definition"
      src="/media/noticeDefinition.svg"
      alt="noticeDefinition"
      v-if="section === 0"
    />
    <safety-rules
      v-if="section === 1"
      :chosenCourse="chosenCourse"
    ></safety-rules>
  </div>
</template>

<script>
import SafetyRules from "./SafetyRules.vue";
export default {
  components: { SafetyRules },
  name: "info-hanging-board",
  props: [
    "section",
    "chosenCourse",
    "flipStart",
    "flipEndDefine",
    "backFlip",
    "flipEndSaftyRules",
  ],
  data() {
    return {
      theInfo: [
        [
          "אז מה זה עגורן עילי?",
          "עגורנים עיליים הם סוגי מנופים נייחים שלא מובנים על רכב, אלא מותקנים בסדנא ונותנים שירות בדרך כלל בפסי ייצור וכדומה.",
          "קיימים 4 דרגות רישיון הפעלה בעגורנים: א-ב, ג-ד.",
        ],
        [
          "כללי בטיחות",
          "ישנם מספר כללי בטיחות אותם יש לבדוק לפני שניגש לביצוע עבודה עם המנוף:",
        ],
      ],
    };
  },
};
</script>

<style scoped>
#info-hanging-board {
  background-repeat: no-repeat;
  background-size: 100% 100%;
  width: 60rem;
  height: 37rem;
  margin-top: 4.2rem;
  z-index: 1;
  display: flex;
  align-items: center;
  flex-direction: column;
  /* transform-style: preserve-3d; */
}

.unfliped-board {
  background-image: url("/media/infoHangBoard/computer/infoHangingBoard.svg");
}

/* .flipBoard {
  transition: transform 1s;
    transform-style: preserve-3d;
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
} */

.flip-end-definition {
  transition: transform 2s;
  transform: rotateY(180deg);
}

.flip-start-safty-rules {
  transition: transform 1s;
  transform: rotateY(0deg);
  background-image: url("/media/infoHangBoard/computer/flipedInfoHangingBoard.svg");
}

.flip-end-safty-rules {
  transition: transform 2s;
  transform: rotateY(-180deg);
}

.flip-start-definition {
  transition: transform 1s;
  transform: rotateY(0deg);
}

.info-container {
  margin-top: 10rem;
  color: white;
  width: 35rem;
  font-size: 1.2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
}

.notice-definition {
  margin-bottom: 2rem;
    margin-right: -0.2rem;
    width: 60.9rem;
}

@media screen and (max-width: 700px) {
  #info-hanging-board {
    width: 29rem;
    height: 46rem;
    justify-content: space-around;
  }

  .unfliped-board {
    background-image: url("/media/infoHangBoard/phone/infoHangingBoard.svg");
  }

  .flip-start-safty-rules {
    background-image: url("/media/infoHangBoard/phone/flipedInfoHangingBoard.svg");
  }

  .text {
    width: 27rem;
  }

  .notice-definition {
    margin-right: -0.1rem;
    width: 30.7rem;
    }
}
</style>
