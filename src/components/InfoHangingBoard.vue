<template>
  <div
    id="info-hanging-board"
    :class="{
      'flip-start-safty-rules': flipStart,
      'flip-end-definition': flipEndDefine,
      'unfliped-board': !flipStart,
      'flip-end-safty-rules': backFlip,
      'flip-start-definition': flipEndSaftyRules,
      'unfliped-board': flipHook,
      'in-winches': inWinches,
      'the-placement': !inWinches,
    }"
  >
    <!-- about definition and safetyrules -->
    <div
      class="add-flex"
      v-if="
        !inWinches && sectionHangingBoard !== 2 && sectionHangingBoard !== 3
      "
    >
      <div class="info-container">
        <p class="header">{{ theInfo[sectionHangingBoard][0] }}</p>
        <p
          v-for="(text, index) in theInfo[sectionHangingBoard].slice(1)"
          :key="index"
          class="info-text"
        >
          {{ text }}
        </p>
        <p v-if="sectionHangingBoard === 1" class="instraction to-show">
          - לחצו על כל הכללים -
        </p>
      </div>
      <img
        class="notice-definition computer-notice"
        src="/media/noticeDefinition/computer/noticeDefinition.svg"
        alt="noticeDefinition"
        v-if="sectionHangingBoard === 0"
      />
      <img
        class="notice-definition phone-notice"
        src="/media/noticeDefinition/phone/noticeDefinition.svg"
        alt="noticeDefinition"
        v-if="sectionHangingBoard === 0"
      />
      <safety-rules
        v-if="sectionHangingBoard === 1"
        :chosenCourse="chosenCourse"
        @showNextBtn="showNextBtnSafetyRules"
      ></safety-rules>
    </div>
    <!-- about winches -->
    <p class="info-in-winches" v-if="inWinches">
      מכשיר המיועד להזיז משאות כבדים באמצעות חבל הנכרך על גבי ציר
    </p>
    <!-- about potentialAdditions -->
    <div
      class="info-container"
      v-if="sectionHangingBoard === 2 || sectionHangingBoard === 3"
    >
      <p class="header">{{ theInfo[sectionHangingBoard][0] }}</p>
      <!-- <div v-if="sectionHangingBoard === 2"> -->
      <potential-additions
        v-if="sectionHangingBoard === 2"
      ></potential-additions>
      <p class="asterisk" v-if="sectionHangingBoard === 2">
        * לא בכל עגורן מצויה תוספת
      </p>
      <!-- </div> -->
      <div class="electrical-system-container" v-if="sectionHangingBoard === 3">
        <p>
          {{ theInfo[sectionHangingBoard][1] }}
        </p>
        <div class="item-container">
          <div
            v-for="(item, index) in titlesInElectricalSystemArr"
            :key="index"
          >
            <img class="icon" alt="icon" :src="'/media/iconsElectricalSystem/icon' + index + '.png'" />
            <p>{{ item }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PotentialAdditions from "./PotentialAdditions.vue";
import SafetyRules from "./SafetyRules.vue";
export default {
  components: { SafetyRules, PotentialAdditions },
  name: "info-hanging-board",
  props: [
    "sectionHangingBoard",
    "chosenCourse",
    "flipStart",
    "flipEndDefine",
    "backFlip",
    "flipEndSaftyRules",
    "flipHook",
    "inWinches",
  ],
  data() {
    return {
      theInfo: [
        [
          "אז מה זה עגורן עילי?",
          "עגורנים עיליים הם סוגי מנופים נייחים שלא מובנים על רכב, אלא מותקנים בסדנא ונותנים שירות בדרך כלל בפסי ייצור וכדומה.",
          "קיימות 4 דרגות רישיון הפעלה בעגורנים: א-ב, ג-ד.",
        ],
        [
          "כללי בטיחות",
          "ישנם מספר כללי בטיחות אותם יש לבדוק לפני שניגש לביצוע עבודה עם המנוף:",
        ],
        ["תוספות פוטנציאליות בעגורנים"],
        ["מערכת החשמל בעגורנים", "אחראית על 3 מערכות עיקריות:"],
      ],
      titlesInElectricalSystemArr: ["הסעה", "פיקוד", "חשמל"],
    };
  },
  methods: {
    showNextBtnSafetyRules() {
      this.$emit("showNextBtnSafetyRules");
    },
  },
};
</script>

<style scoped>
.the-placement {
  width: 60rem;
  height: 37rem;
  margin-top: 4.2rem;
}

#info-hanging-board {
  background-repeat: no-repeat;
  background-size: 100% 100%;
  z-index: 1;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.add-flex {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.in-winches {
  position: absolute;
  width: 40rem;
  height: 17rem;
  bottom: 6.8rem;
  margin-left: -17rem;
  animation: tossAnimation 4s linear infinite;
}

@keyframes tossAnimation {
  0% {
    transform: rotate(0deg);
    margin-left: -17rem;
  }
  25% {
    transform: rotate(-1deg);
    margin-left: -15rem;
  }
  50% {
    transform: rotate(0deg);
    margin-left: -17rem;
  }
  75% {
    transform: rotate(1deg);
    margin-left: -19rem;
  }
  100% {
    transform: rotate(0deg);
    margin-left: -17rem;
  }
}

.info-in-winches {
  margin-top: 9rem;
  color: white;
  width: 15rem;
}

.unfliped-board {
  background-image: url("/media/infoHangBoard/computer/infoHangingBoard.svg");
}

.instraction {
  font-size: 1rem;
  color: #e0f2f4;
  margin: 0rem;
}

.to-show {
  display: none;
}

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
  transform: rotateY(180deg);
  /* background-image: url("/media/infoHangBoard/computer/infoHangingBoard.svg"); */
}

.flip-start-definition {
  transition: transform 1s;
  transform: rotateY(0deg);
}

.info-container {
  margin-top: 10rem;
  color: white;
  /* width: 35rem; */
  width: 50rem;
  font-size: 1.2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
  margin: 0rem;
  margin-top: 2rem;
}

.notice-definition {
  margin-top: 2rem;
  margin-right: -0.2rem;
  width: 56.15rem;
}

.computer-notice {
  display: block;
}

.phone-notice {
  display: none;
}
.info-text {
  margin: 0rem;
  padding: 1rem;
}

.asterisk {
  font-weight: bold;
  position: relative;
  left: 17rem;
}

.item-container {
  width: 100%;
  display: flex;
    justify-content: space-evenly;
    align-items: flex-end;
}

.electrical-system-container {
  width: 100%;
}
@media screen and (max-width: 700px) {
  .the-placement {
    width: 26rem;
    height: 42rem;
    justify-content: space-around;
  }

  .unfliped-board {
    background-image: url("/media/infoHangBoard/phone/infoHangingBoard.svg");
  }

  .flip-start-safty-rules {
    background-image: url("/media/infoHangBoard/phone/flipedInfoHangingBoard.svg");
  }

  .info-text {
    width: 25rem;
  }

  .notice-definition {
    margin-right: -0.1rem;
    width: 29rem;
  }

  .info-container {
    margin-top: 5.9rem;
    width: 26rem;
  }

  .asterisk {
    left: 5rem;
  }

  .computer-notice {
    display: none;
  }

  .phone-notice {
    display: block;
  }

  .notice-definition {
    width: 26.1rem;
  }
  .to-show {
    display: block;
    font-weight: bold;
  }

  .in-winches {
    height: 25rem;
    bottom: 12.8rem;
  }

  @keyframes tossAnimation {
    0% {
      transform: rotate(0deg);
      margin-left: -13rem;
    }
    25% {
      transform: rotate(-1deg);
      margin-left: -11rem;
    }
    50% {
      transform: rotate(0deg);
      margin-left: -13rem;
    }
    75% {
      transform: rotate(1deg);
      margin-left: -15rem;
    }
    100% {
      transform: rotate(0deg);
      margin-left: -13rem;
    }
  }

  .info-in-winches {
    font-size: 1.3rem;
  }

  .icon {
    width: 8rem;
  }
}
</style>
