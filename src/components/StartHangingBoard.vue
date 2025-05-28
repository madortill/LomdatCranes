<template>
  <div
    id="start-hanging-board"
    :class="[!isUp ? 'toss' : 'up', isDown ? 'down' : '']"
  >
    <img src="/media/hook.svg" alt="hook" class="hook" />
    <img
      src="/media/wire.png"
      alt="wire"
      :class="partNum !== 3 && !showSelection ? 'wire' : 'smallWire'"
    />
    <div class="blue-board">
      <p class="lomdatName" v-if="partNum === 1 && !showSelection">
        לומדת עגורנים
      </p>
      <div v-if="partNum === 2">
        <p>הינכם עומדים ללמוד על עגרונים מסוג</p>
        <p class="theCraneKind">{{ craneKind }}</p>
        <p>וכיצד לתפעל אותו</p>
        <p>
         <b> דגש:</b> בסוף הלומדה ישנו מבחן שכדי שיהיה מאופשר ודרכו לקבל ציון עליך לעבור את הלומדה
          מתחילתה
        </p>
        <p class="goodWord">בהצלחה!</p>
        <img
          @click.once="nextBoard"
          class="checkMarkBtn"
          src="/media/containerCheckMarkBtn.png"
          alt="checkMarkBtn"
        />
        <img src="/media/checkMark.png" alt="icon" class="check-mark-icon"/>
      </div>
    </div>
    <div :class="partNum === 1 ? 'add-margin' : ''" v-if="partNum === 1 || partNum === 3 || showSelection">
      <img
        v-if="partNum === 1 && !showSelection"
        src="/media/twoWires.png"
        alt="wire"
        class="twoWires"
      />
      <div class="mini-board" :class="partNum === 3 || showSelection ? 'regular-margin' : 'fix-margin'">{{ arrYellowSign[indexYellowSign] }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "start-hanging-board",
  props: [
    "partNum",
    "craneKind",
    "isUp",
    "isDown",
    "indexYellowSign",
    "showSelection",
  ],
  data() {
    return {
      arrYellowSign: ["בחרו את סוג העגורן ללמידה", "בחרו בחלק הרלוונטי אלייך"],
    };
  },
  methods: {
    nextBoard() {
      this.$emit("toNextBoard");
    },
  },
};
</script>

<style scoped>
#start-hanging-board {
  z-index: 10000;
  /* width: 60vw; */
  width: 100vw;
  height: 50rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* margin-right: 5rem; */
  /* margin-top: 5rem; */
  pointer-events: none;
}

/* 
@keyframes tossAnimation {
  0% {
    transform: rotate(-1deg);
    margin-left: -2rem;
  }
  50% {
    transform: rotate(1deg);
    margin-left: 2rem;
  }
  100% {
    transform: rotate(-1deg);
    margin-left: -2rem;
  }
} */

@keyframes tossAnimation {
  0% {
    transform: rotate(0deg);
    margin-left: 0rem;
  }
  25% {
    transform: rotate(-1deg);
    margin-left: -2rem;
  }
  50% {
    transform: rotate(0deg);
    margin-left: 0rem;
  }
  75% {
    transform: rotate(1deg);
    margin-left: 2rem;
  }
  100% {
    transform: rotate(0deg);
    margin-left: 0rem;
  }
}

.hook {
  width: 3rem;
  z-index: 2;
  margin-top: -0.8rem;
}

.wire {
  height: 1.5rem;
  z-index: 2;
  width: 20rem;
  margin-top: -0.6rem;
}

.smallWire {
  height: 1.5rem;
  z-index: 2;
  width: 10rem;
  margin-top: -0.7rem;
}

.blue-board {
  color: white;
  background-color: #023047;
  /* padding: 1rem; */
  border-radius: 1.5rem;
  width: 30rem;
  position: relative;
}

.lomdatName {
  font-size: 4rem;
  font-weight: 900;
  color: #e0f2f4;
}

.theCraneKind {
  color: #ffb703;
  font-size: 2.5rem;
  margin: 0rem;
}

.goodWord {
  color: #8cd0ec;
  font-size: 1.5rem;
}

.explain-board {
  color: white;
  background-color: #023047;
  padding: 2rem;
  font-size: 1rem;
  border-radius: 1.5rem;
  width: 30rem;
  z-index: 2;
}

.twoWires {
  z-index: 2;
  width: 9rem;
  height: 1rem;
  margin-top: -0.6rem;

}

.mini-board {
  color: #023047;
  background-color: #ffb703;
  padding: 1rem;
  /* font-size: 1rem; */
  border-radius: 0.7rem;
  z-index: 2;
}

.fix-margin {
  margin-top: -0.6rem;
}

.regular-margin {
  margin-top: 0rem;
}

.add-margin {
  margin-top: -0.3rem;
}

.up {
  animation: goingUp 0.6s linear forwards;
}

.toss {
  animation: tossAnimation 4s linear infinite;
}

@keyframes goingUp {
  0% {
    position: relative;
    bottom: 0vh;
  }
  100% {
    position: relative;
    bottom: 80vh;
  }
}

.down {
  animation: goingDown 0.6s linear forwards;
}

@keyframes goingDown {
  0% {
    position: relative;
    bottom: 80vh;
  }
  100% {
    position: relative;
    bottom: 0vh;
  }
}

.checkMarkBtn {
  position: absolute;
  width: 10rem;
  height: 6rem;
  left: 0rem;
  bottom: -0.6rem;
  margin: 0rem;
  padding: 0rem;
  cursor: pointer;
  /* z-index: 1; */
  pointer-events: all;
}

.check-mark-icon {
  position: absolute;
  bottom: 0rem;
left:0rem;
height: 3rem;
/* z-index: 1; */
animation: jump 1s ease-in-out infinite ;
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


@media screen and (max-width: 600px) {
  .blue-board {
    width: 26rem;
  }
}
</style>
