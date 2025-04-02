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
        v-if="!isClickedQuestionMark"
        class="num"
        v-for="num in numArr"
        :key="num"
      >
        {{ num }}
      </p>
      <p v-if="isClickedQuestionMark" class="num">3</p>
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
      }
    },
  },
};
</script>

<style scoped>
#crane-operations {
  margin-top: -2rem;
}

.the-info {
  width: 18rem;
}

.header {
  font-size: 1.8rem;
  text-align: center;
  font-weight: bold;
}

.bubble {
  background-color: white;
  border-radius: 1rem;
  padding: 1rem;
  width: 25rem;
  position: relative;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  align-items: center;
}

.bubble-container {
  display: flex;
  height: 24rem;
  flex-direction: column;
  justify-content: space-evenly;
}

.numbers-container {
  position: absolute;
  top: 15rem;
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
  margin-top: 2.6rem;
  margin-bottom: 0rem;
}

.orange-bubble {
  background-color: #f88c01;
  position: absolute;
  top: -1rem;
  left: -1rem;
  width: 5rem;
  height: 5rem;
  border-radius: 100%;
  /* z-index: 100; */
  cursor: pointer;
}

.more-info-bubble {
  height: 20rem;
  position: absolute;
  /* transition: all 1s; */
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
  margin-bottom: 7rem;
}
</style>
