<template>
  <div id="info-hanging-board">
    <!-- <img class="board" src="../../src/assets/media/infoHangingBoard.png" alt="infoHangingBoard"/> -->
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
      src="../../src/assets/media/noticeDefinition.svg"
      alt="noticeDefinition"
      v-if="section === 0"
    />
  </div>
</template>

<script>
export default {
  name: "info-hanging-board",
  props: ["section"],
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
  background-image: url("../../src/assets/media/infoHangingBoard_1.svg");
  background-repeat: no-repeat;
  background-size: 100% 100%;
  width: 60rem;
  height: 37rem;
  margin-top: 5rem;
  z-index: 1;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.info-container {
  margin-top: 10rem;
  color: white;
  width: 35rem;
  font-size: 1.2rem;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
}

.notice-definition {
  margin-bottom: 0rem;
  margin-right: -0.2rem;
  width: 56.2rem;
  /* height: 3rem; */
}

/*  */
</style>
