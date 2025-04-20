<template>
  <div id="winches">
    <p class="header">כננות</p>
    <p class="sub-title">{{ subTitle[part] }}</p>
    <p v-if="part === 1">{{ typesInfo }}</p>

    <div class="definition-container" v-if="part === 0">
        <p class="text-in-btn">רגע מהי כננת?</p>
      <img :class="!isClicked ? 'with-animation' : '' " @click="showBoard" class="definition-btn" src="/media/winchPage/btn.png" alt="btn" />
      <img class="legs" src="/media/winchPage/legs.png" alt="legs" />
    </div>

    <div v-if="part === 1"></div>
    <p></p>
  </div>
</template>

<script>
export default {
  name: "winches",
  //   props: [""],
  data() {
    return {
      subTitle: ["הגדרה", "סוגים"],
      typesInfo:
        "ישנם כננות מסוג כבל ומסוג שרשרת הרמה.כל אחת מהן יכולה להיות מופעלת בצורה מכאנית (ידנית) ובצורה חשמלית.",
      part: 0,
      isClicked: false,
    };
  },
  methods: {
    showBoard() {
        this.$emit('show-tiny-board');
        this.isClicked = true;
    }
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
    z-index: 1;
    font-size: 1.4rem;
    margin-right: -15rem;
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
