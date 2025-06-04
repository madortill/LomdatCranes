<template>
  <div id="crane-operations">
    <p class="header">פעולות העגורן</p>
    <div class="bubble-container">
      <div
        v-for="(info, index) in arrinfo"
        :key="index"
        class="bubble"
        :class="
          index === 2 && isClickedQuestionMark && this.craneKind === 'עגורן שער'
            ? 'more-info-bubble'
            : ''
        "
      >
        <p class="the-info">{{ info }}</p>
        <ul class="fix-position" type="circle" v-if="index === 2 && this.craneKind === 'עגורן גשר'">
          <li> מנוע להרמת והורדת כבל כננת</li>
          <li> מנוע למערכת הסעה של כננת ההרמה</li>
          <li> שני מנועים שעובדים במקביל ומסיעים את קורת העגורן</li>
        </ul>

        <div
          :class="
            index === 2 &&
            isClickedQuestionMark &&
            this.craneKind === 'עגורן שער'
              ? 'more-info'
              : 'hide'
          "
        >
          <hr class="line" />
          העגורן נע על מסילות חשמליות מה שמאפשר להזיז את קורת העגורן אחורה
          וקדימה לכל אורך שטח המסילות.
        </div>
        <div
          @click="showMoreInfo"
          class="orange-bubble"
          v-if="index === 2 && this.craneKind === 'עגורן שער'"
        >
          <p
            class="question-mark icon-orange-bubble"
            v-if="!isClickedQuestionMark"
          >
            ?
          </p>
          <p class="icon-orange-bubble" v-else>X</p>
        </div>
      </div>
    </div>
    <div class="numbers-container">
      <p
        class="num"
        :class="{
          'animation-for-three':
            num === 3 && isClickedQuestionMark && craneKind === 'עגורן שער',
          'fade-animation':
            num !== 3 && isClickedQuestionMark && craneKind === 'עגורן שער',
        }"
        v-for="num in numArr"
        :key="num"
      >
        {{ num }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "crane-operations",
  props: ["craneKind"],
  data() {
    return {
      numArr: [1, 2, 3],
      isClickedQuestionMark: false,
    };
  },
  computed: {
    arrinfo() {
      let arr = ["תנועת כננת לאורך הקורה", "הרמה והורדה של כבל כננת", ""];
      switch (this.craneKind) {
        case "עגורן גשר":
          arr[2] = "בעגורן גשר סטנדרטי ישנם 4 מנועים חשמליים:";
          break;
        case "עגורן שער":
          arr[2] = 'תנועת כל העגורן קדימה ואחורה ע"י גלגלי הסעה בתוך המסילות';
          break;
        case "עגורן עמוד":
          arr[2] = 'תנועת הקורה ימינה ושמאלה ע"י צידוד';
          break;
        default:
          arr = ["מידע לא זמין."];
      }
      return arr;
    },
  },
  methods: {
    showMoreInfo() {
      if (this.isClickedQuestionMark) {
        this.isClickedQuestionMark = false;
      } else {
        this.isClickedQuestionMark = true;
        this.$emit('show-next-btn');
      }
    },
  },
};
</script>

<style scoped>
#crane-operations {
  margin-top: -2rem;
}

ul {
  padding-left: 1.7rem; /* Adjust padding for the list items */
}
li::before {
  content: "\2022"; /* Unicode for a bullet character */
}

.circle-list {
  padding-left: 20px;
  list-style-type: circle; /* This creates circle bullets for the list */
}

.the-info {
  width: 17rem;
  margin: 1rem;
}

.header {
  font-size: 1.8rem;
  text-align: center;
  font-weight: bold;
}

.bubble {
  background-color: white;
  border-radius: 1rem;
  width: 25rem;
  position: relative;
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
  align-items: center;
  margin-bottom: 1.4rem;
}

.bubble-container {
  height: 24rem;
  flex-direction: column;
  justify-content: space-evenly;
}

.numbers-container {
  position: absolute;
  top: 14.5rem;
}

.hide {
  display: none;
}

.more-info {
  display: block;
}

.num {
  font-size: 3rem;
  font-family: Secular-One;
  margin-top: 1.1rem;
  margin-bottom: 0rem;
}

.animation-for-three {
  z-index: 2;
  position: relative;
  animation: growUpNum 0.3s linear forwards;
}

.fade-animation {
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

.orange-bubble {
  background-color: #f88c01;
  position: absolute;
  top: -1rem;
  left: -1rem;
  width: 5rem;
  height: 5rem;
  border-radius: 100%;
  cursor: pointer;
}

.more-info-bubble {
  height: 0rem;
  position: absolute;
  top: 17.9rem;
  animation: growUpDiv 0.3s linear forwards;
  bottom: 0;
  z-index: 2;
}

@keyframes growUpDiv {
  0% {
    height: 0rem;
    top: 28.9rem;
  }
  100% {
    height: 17rem;
    top: 17.9rem;
  }
}

@keyframes growUpNum {
  0% {
    bottom: 0rem;
  }
  100% {
    bottom: 11rem;
  }
}

.icon-orange-bubble {
  font-weight: bold;
  font-size: 2rem;
  margin-left: 1rem;
  margin-top: 1.5rem;
  font-family: Secular-One;
}

.question-mark {
  animation: jump 1s ease-in-out infinite;
}

@keyframes jump {
  0% {
    transform: translateY(0); /* Start at the original position */
  }
  25% {
    transform: translateY(-10px); /* Move up a bit */
  }
  50% {
    transform: translateY(0); /* Go back to the original position */
  }
  75% {
    transform: translateY(-5px); /* Slightly move up */
  }
  100% {
    transform: translateY(0); /* Return to original position */
  }
}

.line {
  width: 10rem;
  border: none;
  border-top: 0.2rem solid black; /* Adjust the thickness of the line */
  margin-bottom: 4rem;
}

.fix-position {
  margin-top: -1rem;
}
</style>
