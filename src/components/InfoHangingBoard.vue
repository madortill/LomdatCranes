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
      <potential-additions
        v-if="sectionHangingBoard === 2"
      ></potential-additions>
      <p class="asterisk" v-if="sectionHangingBoard === 2">
        * לא בכל עגורן מצויה תוספת
      </p>
      <div class="electrical-system-container" v-if="sectionHangingBoard === 3">
        <p>
          {{ theInfo[sectionHangingBoard][1] }}
        </p>

        <div class="item-container">
          <div
            v-for="(item, index) in titlesInElectricalSystemArr[0]"
            :key="index"
            class="mini-item-container"
          >
            <p class="item-title">{{ item }}</p>
            <img class="icon" alt="icon" :src="getIconUrl(index)" />
            <p class="fix-width">{{ titlesInElectricalSystemArr[1][index] }}</p>
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
        [
          "מערכת החשמל בעגורנים",
          "ישנם 3 מערכות חשמל בעגורן עילי, כל מערכת אחראית על דבר אחר בעגורן:",
          "",
        ],
      ],
      titlesInElectricalSystemArr: [
        ["הסעה", "פיקוד", "חשמל"],
        [
          "אחראית על תנועת העגורן לאורך המסילות באופן חשמלי",
          "יש כמה שיטות פיקוד שנלמד עליהם בהמשך אשר מאפשרות הפעלה של העגורן",
          "מספקת אנרגיה והפעלה של העגורן",
        ],
      ],
    };
  },
  methods: {
    showNextBtnSafetyRules() {
      this.$emit("showNextBtnSafetyRules");
    },
    getIconUrl(num) {
      // Determine the base URL (for local and production)
      const basePath =
        process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return `${basePath}media/iconsElectricalSystem/icon${num}.png`; // Static path to the images in the public folder
    },
  },
  computed: {},
};
</script>

<style scoped>
.item-title {
  font-weight: bold;
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.mini-item-container {
  border: 4px solid white;
  border-radius: 1rem;
}

.fix-width {
  width: 10rem;
}

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
  bottom: 5.9rem;
  margin-left: -15.5rem;
  animation: tossAnimation 4s linear infinite;
}

@keyframes tossAnimation {
  0% {
    transform: rotate(0deg);
    margin-left: -15.5rem;
  }
  25% {
    transform: rotate(-1deg);
    margin-left: -13.5rem;
  }
  50% {
    transform: rotate(0deg);
    margin-left: -15.5rem;
  }
  75% {
    transform: rotate(1deg);
    margin-left: -17.5rem;
  }
  100% {
    transform: rotate(0deg);
    margin-left: -15.5rem;
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
}

.flip-start-definition {
  transition: transform 1s;
  transform: rotateY(0deg);
}

.info-container {
  margin-top: 10rem;
  color: white;
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
  align-items: flex-start;
  position: relative;
}

.electrical-system-container {
  width: 100%;
}

.icon {
  position: absolute;
  top: 0rem;
  margin-right: 2rem;
  transform: rotate(-13deg);
  height: 5rem;
  background-color: white;
  border-radius: 4rem;
}
@media screen and (max-width: 700px) {
  .item-title {
    margin-bottom: 0.3rem;
    margin-top: 0.4rem;
  }

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
    height: 21rem;
    bottom: 9.1rem;
    margin-left: -12.5rem;
    animation: tossAnimation 2.5s linear infinite;
  }

  @keyframes tossAnimation {
    0% {
      transform: rotate(0deg);
      margin-left: -12.5rem;
    }
    25% {
      transform: rotate(-1deg);
      margin-left: -11.5rem;
    }
    50% {
      transform: rotate(0deg);
      margin-left: -12.5rem;
    }
    75% {
      transform: rotate(1deg);
      margin-left: -13.5rem;
    }
    100% {
      transform: rotate(0deg);
      margin-left: -12.5rem;
    }
  }

  .info-in-winches {
    font-size: 1.3rem;
    width: 12rem;
  }

  .icon {
    height: 5rem;
    position: static;
    border-radius: 0rem;
    background-color: #023047;
    transform: rotate(0deg);
    margin-right: 0rem;
    margin-top: -0.6rem;
  }

  .fix-width {
    width: 7rem;
    margin-top: -0.4rem;
  }

  .item-container {
    margin-top: -1rem;
  }

  .mini-item-container {
    border: 2px solid white;
    width: 7.9rem;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
</style>
