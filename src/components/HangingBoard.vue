<template>
<div id="hanging-board" :class="[!isUp ? 'toss' : 'up', isDown ? 'down' : '']">
  <img src="/media/hook.svg" alt="hook" class="hook"/>
        <img src="/media/wire.png" alt="wire" :class="partNum !== 3 && !showSelection ? 'wire' : 'smallWire'"/>
        <div class="blue-board">
            <p class="lomdatName" v-if="partNum === 1 && !showSelection">לומדת עגורנים</p>
            <div v-if="partNum === 2">
                <p>הינכם עומדים ללמוד על עגרונים מסוג</p>
                <p class="theCraneKind">{{craneKind}}</p>
                <p>וכיצד לתפעל אותו</p>
                <p>דגש: בסוף הלומדה ישנו תרגול שכדי לקבל ציון עליך לעבור את הלומדה מתחילתה</p>
                <p class="goodWord">בהצלחה!</p>
                <img @click.once="nextBoard" class="checkMarkBtn" src="/media/checkMarkBtn.png" alt="checkMarkBtn"/>
            </div>
        </div>
        <div v-if="partNum === 1 || partNum === 3 || showSelection">
            <img v-if="partNum === 1 && !showSelection" src="/media/twoWires.png" alt="wire" class="twoWires"/>
            <div class="mini-board">{{arrYellowSign[indexYellowSign]}}</div>
        </div>            
    </div>
</template>

<script>
    export default {
        name: "hanging-board",
        props: ["partNum", "craneKind", "isUp", "isDown", "indexYellowSign", "showSelection"],
        data() {
            return {
              arrYellowSign: ["בחרו את סוג העגורן ללמידה", "בחרו בחלק הרלוונטי אלייך"],
            };
        },
        methods: {
          nextBoard(){
            this.$emit('toNextBoard');
            console.log('hi');
          },
        },
};
</script>

<style scoped>

#hanging-board{
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

@keyframes tossAnimation {
  0% {
    transform: rotate(-1deg);
    margin-left: -3rem;
  }
 50% {
  transform: rotate(1deg);
    margin-left: 3rem;
 }
  100% {
    transform: rotate(-1deg);
    margin-left: -3rem;
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
  width:20rem;
  margin-top: -0.6rem;
}

.smallWire {
  height: 1.5rem;
  z-index: 2;
  width:10rem;
  margin-top: -0.7rem;
}

.blue-board {
  color: white;
  background-color: #023047;
  /* padding: 1rem; */
  border-radius: 1.5rem;
  width:30rem;
  position: relative;
}

.lomdatName {
  font-size: 4rem;
  font-weight: 900;
  color: #E0F2F4;
}

.theCraneKind {
    color: #FFB703;
    font-size: 2.5rem;
    margin: 0rem;
}

.goodWord {
    color: #8CD0EC;
    font-size: 1.5rem;
}

.explain-board {
  color: white;
  background-color: #023047;
  padding: 2rem;
  font-size: 1rem;
  border-radius: 1.5rem;
  width:30rem;
  z-index: 2;
}

.twoWires {
  z-index: 2;
  width: 9rem;
  height:1rem;
}

.mini-board {
  color: #023047;
  background-color: #FFB703;
  padding: 1rem;
  font-size: 1rem;
  border-radius: 0.7rem;
  z-index: 2;
  margin-top: -0.2rem;
}

.up {
  animation: goingUp 0.6s linear forwards;
}

.toss {
    animation: tossAnimation 4s ease-in-out infinite;
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
  margin:0rem;
  padding: 0rem;
  cursor: pointer;
  z-index: 65;
  pointer-events: all;
}

</style>