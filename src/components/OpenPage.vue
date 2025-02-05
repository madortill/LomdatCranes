
=<template>
    <div id="open-page">
        <button @click="showInfo" class="info-btn btn">i</button>
        <img class="bahadSymbol" src="../../src/assets/media/bahadSymbol.png" alt="bahadSymbol"/>
        <img class="tillLogo" src="../../src/assets/media/whiteMadorTill.png" alt="tillLogo"/>
        <div class="info-container" v-if= "isOpenInfo"> 
          <p @click="hideInfo" class="close-info">X</p>
            <ul class="info-list">
                <li class="info" v-for="(subTitle, title) in infoObject" :key="title">
                  <span class="info-title">{{ title }}</span><br>
                  <span>{{ subTitle }}</span>
                </li>
            </ul>
        </div>
        <div class="start-container" v-if="!isOpenInfo">
            <img src="../../src/assets/media/Crane.png" alt="crane" class="bgCrane"/>
            <div class="start-sign">
              <img src="../../src/assets/media/hook.svg" alt="hook" class="hook"/>
              <img src="../../src/assets/media/wire.png" alt="wire" class="wire"/>
              <div class="board">לומדת עגורנים</div>
              <img src="../../src/assets/media/twoWires.png" alt="wire" class="twoWires"/>
              <div class="mini-board">בחרו את סוג העגורן ללמידה </div>
        </div>
            

            
            
            <div class="box-container">
              <Box class="box btn" newTitle="עילי" ></Box>
              <Box class="box btn" newTitle="העמסה עצמית"></Box>
            </div>
        </div>
        <div class="ground"></div>
    </div>
</template>

<script>
import Box from '../../src/components/Box.vue';
    export default {
        name: "open-page",
        components: {Box},
        data() {
            return {
              infoObject: {
                    "מפתחת לומדה:": 'רב"ט דני שריקי',
                    "גרפיקאית:": 'רב"ט קריסטינה ברחטוב',
                    "מומחה תוכן:": 'רס"ר יוחאי עזרא',
                    'רמ"ד טי"ל:': 'רס"מ שלומי אוגרן',
                    "גרסה:": "ינואר 2025"
                },
                isOpenInfo: false,
            };
          },
        methods: {
          showInfo() {
            this.isOpenInfo = true;
          },
          hideInfo() {
            this.isOpenInfo = false;
          }
        },
    };
</script>

<style scoped>
#open-page {
  direction: rtl;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100vw;
  flex-direction: column;
  color: #023047;
  background-image: url("../../src/assets/media/cloudsBg.svg");
  background-size: 100vw 100vh;
  background-repeat: no-repeat;
 
}

  .title {
    font-weight: bolder;
    font-size: 6rem;
    animation: floatAnimation 3s ease-in-out infinite;
  }

  @keyframes floatAnimation {
    0% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(12px);
    }
    100% {
      transform: translateY(0);
    }
  }

.btn {
    cursor: pointer;
    pointer-events: visibleStroke;
}

  .box {
    width: 20rem;
    z-index: 1;
    margin: 2rem;
  }

  .start-sign {
    width: 100vw;
    height: 40rem;
    display: flex;
    flex-direction: column;
    align-items: center;
     animation: tossAnimation 3s ease-in-out infinite;
     transform: rotate(-1deg);
    margin-right: 5rem;
    pointer-events: none;
  }

  .box-container {
    width: 100vw;
    display:flex;
    z-index: 1;
    justify-content: space-evenly;
  }

  @keyframes tossAnimation {
  0% {
    transform: rotate(-1deg);
    margin00000-right: 5rem;
  }
 50% {
  transform: rotate(1deg);
    margin-left: 5rem;
 }
  100% {
    transform: rotate(-1deg);
    margin-right: 5rem;
  }
}

.info-btn {
  border: 3px solid #FFB703;
  background-color: #FFB703;
  color: #E0F2F4;
  border-radius: 100%;
  width: 2rem;
  height: 2rem;
  padding: 0.2rem;
  font-size: 1rem;
  position: absolute;
  left: 6rem;
  top: 1rem;
  font-weight: bold;
}

.info-btn:hover {
    animation: fade 0.2s linear forwards;
  }

  @keyframes fade {
    0% {
      border: 3px solid #FFB703;
      background-color: #FFB703;
    }
    100% {
        background-color: #023047;
        border: 3px solid #023047;
    }
  }


.info-container {
  background-color: white;
  color:#023047;
  border-radius: 2rem;
  width: 27rem;
  height: 27rem;
  animation: windowShow 0.2s linear forwards;
  font-size: 1.5rem;
}

.info-list {
  display: flex;
  width: 100%;
  margin-top: -3rem;
  padding: 0%;
  flex-direction: column;
}

.info-title {
  font-weight: bold;
}

.info {
  margin-bottom: 1.2rem;
}

.close-info {
  margin-left: 22rem;
  cursor: pointer;
  font-size: 1.8rem;
}

@keyframes windowShow {
    0% {
      height: 25rem;
        width: 25rem; 
        font-size: 1rem;
    }
    100% {
      height: 27rem;
      width: 27rem;
      font-size: 1.2rem;
    }
  }

.bahadSymbol {
  width:4rem;
  position: absolute;
  top: 1rem;
  left: 1rem;
}

.tillLogo {
  position: absolute;
  right: 1rem;
  bottom: 1rem;
  width:4rem;
  z-index: 2;
}

.bgCrane {
    position: absolute;
    right: -11rem;
    width: 38rem;
    height: 100vh;
    pointer-events: none;
}

.start-container {
  width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: space-between;
}

.ground {
  background-color: #023047;
  position: absolute;
  bottom: 0rem;
  width: 100vw;
  height: 9rem;
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

.board {
  color: #E0F2F4;
  background-color: #023047;
  padding: 2rem;
  font-size: 4rem;
  font-weight: 900;
  border-radius: 1.5rem;
  width:30rem;
  /* position:absolute;
  top: 8.9rem; */
  z-index: 2;
  /* border: 3px solid #023047; */
}

.twoWires {
  /* position:absolute;
  top: 18.6rem; */
  z-index: 2;
  width: 9rem;
  height:1rem;
}

.mini-board {
  color: #023047;
  background-color: #FFB703;
  padding: 1rem;
  font-size: 1rem;
  /* font-weight: 900; */
  border-radius: 0.7rem;
  /* position:absolute;
  top: 19.5rem; */
  z-index: 2;
  margin-top: -0.2rem;
  /* border: 3px solid #023047; */
}

@media screen and (max-width:768px){
  .ground {
    height: 15rem;
}

.box {
    width: 20rem;
    z-index: 1;
    margin-bottom: 5rem;
  }
}
</style>