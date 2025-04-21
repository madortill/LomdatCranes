<template>
  <div id="winches">
    <p class="header">כננות</p>
    <p class="sub-title">{{ subTitle[partInWinches] }}</p>

    <div class="definition-container" v-if="partInWinches === 0">
      <p class="text-in-btn">רגע מהי כננת?</p>
      <img
        :class="!isClicked ? 'with-animation' : ''"
        @click="showBoard"
        class="definition-btn"
        src="/media/winchPage/btn.png"
        alt="btn"
      />
      <img class="legs" src="/media/winchPage/legs.png" alt="legs" />
    </div>

    <div v-if="partInWinches === 1">
      <p v-for="item in typesInfo" :key="item">{{ item }}</p>

      <winch-sign-svg :side="'right'"></winch-sign-svg>
      <winch-sign-svg :side="'left'"></winch-sign-svg>
    </div>
  </div>
</template>

<script>
import WinchSignSvg from './WinchSignSvg.vue';
export default {
  components: { WinchSignSvg },
  name: "winches",
  props: ["partInWinches"],
  data() {
    return {
      subTitle: ["הגדרה", "סוגים"],
      typesInfo: [
        "ישנם כננות מסוג כבל ומסוג שרשרת הרמה.",
        "כל אחת מהן יכולה להיות מופעלת בצורה מכאנית (ידנית) ובצורה חשמלית.",
      ],
      //   part: 0,
      isClicked: false,
      sideTurn: 'right',
    };
  },
  methods: {
    showBoard() {
      this.$emit("show-tiny-board");
      this.isClicked = true;
    },
  },
};
</script>

<style scoped>
#winches {
  width: 100vw;
  /* height: 77vh; */
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
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  bottom: 0rem;
  width: 100vw;
}

.definition-btn {
  width: 35rem;
  margin-bottom: -1rem;
  /* animation: growAndShrink 2s infinite ease-in-out; */
  transition: transform 0.3s ease;
  cursor: pointer;
  z-index: 1;
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
  margin-bottom: -3rem;
  z-index: 2;
  font-size: 1.4rem;
  margin-right: -15rem;
  cursor: pointer;
}

.legs {
  width: 30rem;
}

@media screen and (max-width: 700px) {
  .legs {
    width: 20rem;
    height: 38rem;
  }

  .definition-btn {
    width: 28rem;
    margin-bottom: -1rem;
  }
}
</style>
