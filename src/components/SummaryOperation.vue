<template>
  <div id="summary-operation">
    <div class="info-container" :class="indexArr === 1 ? 'change-width' : ''">
      <div v-if="indexArr === 1" class="notice-close-crane">
        <p class="right-part-notice">לשים לב</p>
        <p class="left-part-notice">
          כמפעיל חלה עליך החובה החוקית לוודא כי העגורן נעול בסיום השימוש!
        </p>
      </div>
      <div v-if="indexArr !== 2">
        <p class="header">{{ infoArr[indexArr] }}</p>
        <div
          v-for="(info, index) in stepsArr[indexArr]"
          :key="index"
          class="bubble"
        >
          <p class="num">
            {{ index + 1 }}
          </p>
          <p class="the-step">{{ info }}</p>
        </div>
      </div>
      <div class="black-shadow" v-if="showNotice"></div>
      <div class="notice" v-if="showNotice">
        <p class="close-info" @click="closeNotice">X</p>
        <p class="header-notice">שימו לב!</p>
        <p>בעת סיום העבודה עם העגורן עלייך לחזור על השלבים <b>בסדר ההפוך</b></p>
      </div>
      <div v-if="indexArr === 2" class="finish-container">
        <p>עכשיו אתם יכולים להתחיל את העבודה ולתפעל את עגורן הגשר</p>
        <p class="good-word">כל הכבוד!</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "summary-operation",
  props: ["indexArr", "showNotice"],
  data() {
    return {
      infoArr: [
        "לסיכום שלבי ההפעלה של עגורן גשר:",
        "למעשה שלבי סגירת עגורן הגשר:",
      ],
      stepsArr: [
        [
          "פתיחת זרם חשמל ראשי",
          "הוצאת השלט",
          "שחרור פטריית החירום",
          "שחרור העגורן מנקודת האחסון",
          "חיבור המטען",
        ],
        [
          "שחרור המטען",
          "החזרת העגורן לנקודת האחסון",
          "לחיצת פטריית החירום",
          "הכנסת השלט לנקודת האחסון",
          "סגירת זרם חשמל ראשי",
        ],
      ],
    };
  },
  methods: {
    closeNotice() {
      this.$emit("hide-show-notice", false);
    },
  },
};
</script>

<style scoped>
#summary-operation {
  display: flex;
  color: white;
  height: 100%;
  width: 100vw;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.notice-close-crane {
  background-color: #8cd0ec;
  color: #023047;
  width: 8rem;
  display: flex;
  align-items: center;
  flex-direction: column;
  height: 100%;
  position: relative;
}

.right-part-notice {
  background-color: #ffb703;
  height: 5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 100%;
  width: 6rem;
  font-weight: bold;
}

.left-part-notice {
  padding: 0.5rem;
}

.close-info {
  cursor: pointer;
  font-size: 1.8rem;
  position: absolute;
  right: 1rem;
  top: -1rem;
}

.black-shadow {
  background-color: black;
  opacity: 0.5;
  width: 100%;
  height: 100%;
  position: absolute;
  z-index: 2;
}

.info-container {
  transition: height 0.3s ease, width 0.3s ease;
  background-color: #023047;
  border-radius: 1rem;
  width: 34rem;
  height: 31rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
}

.change-width {
  width: 40rem;
  flex-direction: row;
  align-items: center;
}

.the-step {
  background-color: white;
  border-radius: 1rem;
  width: 25rem;
  height: 3rem;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  margin-bottom: 1.4rem;
  color: black;
}

.bubble {
  width: 34rem;
  height: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
}

.bubble-container {
  height: 24rem;
  flex-direction: column;
  justify-content: space-evenly;
}

.num {
  color: #ffb703;
  font-weight: bold;
  font-size: 2.3rem;
  margin-left: -1.3rem;
  z-index: 2;
  margin-top: -0.8rem;
  font-family: Secular-One;
}

.header {
  margin: 1rem;
  font-size: 1.8rem;
}

.notice {
  background-color: white;
  color: black;
  width: 100%;
  position: absolute;
  z-index: 2;
}

.header-notice {
  color: #8cd0ec;
  font-weight: bold;
  font-size: 1.8rem;
}

.good-word {
  color: #ffb703;
  font-weight: bold;
  font-size: 2.3rem;
}

@media screen and (max-width: 600px) {
  .info-container {
    width: 30rem;
    height: 36rem;
   
  }

  .change-width {
    height: 38rem;
    flex-direction: column;
    justify-content: flex-start;
  }

  .notice-close-crane {
    height: 6rem;
    width: 100%;
    align-items: center;
    flex-direction: row;
  }

  .right-part-notice {
   padding: 0.2rem;
   width: 7rem;
   margin-right: 1rem;
  }
}
</style>
