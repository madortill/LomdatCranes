
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
            <img src="../../src/assets/media/hook.svg" alt="hook" class="hook"/>
            <div class="box-container">
              <Box class="box btn" newTitle="עילי"></Box>
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
}
  /* .start-btn {
    height: 4rem;
    border-radius: 100px;
    min-width: 9rem;
    font-size: 1.7rem;
  } */


  .box {
    /* position: absolute;
    top: -1rem; */
    /* width: 11rem; */
    /* animation: tossAnimation 3s ease-in-out infinite; */
    width: 15rem;
    z-index: 1;
    /* margin: 2rem; */
  }

  .box-container {
    width: 40rem;
    /* position: absolute; */
    display:flex;
    bottom: 0rem;
    z-index: 1;
    justify-content: space-evenly;
   /* left: 50%;
   transform: translateX(-50%);  */
   padding: 2rem;
  }

  @keyframes tossAnimation {
  0% {
    transform: rotate(7deg);
    right: 7rem;
  }
  50% {
    transform: rotate(-7deg);
    right: 4rem;
  }
  100% {
    transform: rotate(7deg);
    right: 7rem;
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
  width: 25rem;
  height: 25rem;
  margin: auto;
  position: absolute;
  animation: windowShow 0.2s linear forwards;
  font-size: 1rem;
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
  margin-bottom: 1rem;
}

.close-info {
  margin-left: 20rem;
  cursor: pointer;
  font-size: 1.8rem;
}

@keyframes windowShow {
    0% {
      height: 20rem;
        width: 20rem; 
        font-size: 0.9rem;
    }
    100% {
      height: 25rem;
      width: 25rem;
      font-size: 1rem;
    }
  }

  .tapes {
    position: absolute;
    left: 0rem;
    bottom: 0rem;
    width: 41rem;
    pointer-events: none;
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
    /* top: -2rem; */
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
}


</style>