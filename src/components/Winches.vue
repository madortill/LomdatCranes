<template>
  <div id="winches">
    <p class="header">כננות</p>
    <p class="sub-title">{{ subTitle[partInWinches] }}</p>
    <!-- first part -->
    <div
      :class="!isClickedWinchImg ? 'with-animation' : ''"
      class="definition-container"
      v-if="partInWinches === 0"
    >
      <p class="text-in-btn">רגע מהי כננת?</p>
      <img
        @click="showBoard"
        class="definition-btn"
        src="/media/winchPage/winch.png"
        alt="btn"
      />
    </div>
    <!-- second part -->
    <div v-if="partInWinches === 1">
      <p v-for="item in typesInfo" :key="item">{{ item }}</p>

      <winch-sign-svg
        @show-pop-out="showPopOut"
        :side="'right'"
        :clickedOnBtnSign="clickedOnBtnSign"
        :learnedBtnsArr="learnedInWinchSign"
      ></winch-sign-svg>
      <winch-sign-svg
        @show-pop-out="showPopOut"
        :side="'left'"
        :clickedOnBtnSign="clickedOnBtnSign"
        :learnedBtnsArr="learnedInWinchSign"
      ></winch-sign-svg>

      <pop-out-winch
        @finish-learning="finishBtnInSign"
        @close-pop-out="closePopOut"
        v-if="ifShowPopOut"
        :title="titleToPopOut"
        :indexTypes="indexClickedTtype"
      ></pop-out-winch>
    </div>
  </div>
</template>

<script>
import PopOutWinch from "./PopOutWinch.vue";
import WinchSignSvg from "./WinchSignSvg.vue";
export default {
  components: { WinchSignSvg, PopOutWinch },
  name: "winches",
  props: ["partInWinches", "isClickedWinchImg", "learnedInWinchSign"],
  data() {
    return {
      subTitle: ["הגדרה", "סוגים"],
      typesInfo: [
        "ישנם כננות מסוג כבל ומסוג שרשרת הרמה.",
        "כל אחת מהן יכולה להיות מופעלת בצורה מכאנית (ידנית) ובצורה חשמלית.",
      ],
      titleToPopOut: "",
      indexClickedTtype: -1,
      ifShowPopOut: false,
      clickedOnBtnSign: false,
    };
  },
  methods: {
    showBoard() {
      this.$emit("show-tiny-board");
    },
    showPopOut(title) {
      this.ifShowPopOut = true;
      this.clickedOnBtnSign = true;

      this.titleToPopOut = title;
      switch (title) {
        case "כננת מכאנית לכבל": {
          this.indexClickedTtype = 0;
          break;
        }
        case "כננת מכאנית לשרשרת": {
          this.indexClickedTtype = 1;
          break;
        }
        case "כננת חשמלית לשרשרת": {
          this.indexClickedTtype = 2;
          break;
        }
        case "כננת חשמלית לכבל": {
          this.indexClickedTtype = 3;
          break;
        }
      }
    },
    closePopOut() {
      this.ifShowPopOut = false;
      this.clickedOnBtnSign = false;
    },
    finishBtnInSign(index) {
      this.$emit("add-learned-winch-in-sign", index);
    },
  },
};
</script>

<style scoped>
#winches {
  width: 100vw;
  margin-top: 5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
}

.sub-title {
  font-size: 1.8rem;
  text-align: center;
  font-weight: bold;
  margin-top: -1rem;
}

.definition-container {
  margin-top: 0rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  bottom: 0rem;
  width: 100vw;
  height: 65%;
  justify-content: flex-end;
}

.definition-btn {
  width: 35rem;
  margin-bottom: -2rem;
  transition: transform 0.3s ease;
  cursor: pointer;
}

.with-animation {
  animation: growAndShrink 2s infinite ease-in-out;
}

@keyframes growAndShrink {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}

.text-in-btn {
  margin-bottom: -5rem;
  z-index: 2;
  font-size: 1.4rem;
  margin-right: -15rem;
  cursor: pointer;
  pointer-events: none;
}

@media screen and (max-width: 700px) {
  .definition-btn {
    width: 27rem;
    height: 40rem;
  }

  .definition-container {
    height: 80%;
  }

  .text-in-btn {
    margin-bottom: -7rem;
  }
}
</style>
