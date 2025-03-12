
<template>
    <div id="open-page">
        <button @click="showInfo" class="info-btn btn">i</button>
        <img class="tillLogo" src="/media/whiteMadorTill.png" alt="tillLogo"/>
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
            <img src="/media/Crane.png" alt="crane" class="bgCrane"/>

            <HangingBoard @toNextBoard="toNextScreen" :indexYellowSign="indexYellowSign" :showSelection="showSelection" :partNum="boardNum" :craneKind="chosenCrane" :isUp="isUp" :isDown="isDown"/>

            <div class="box-container"  v-if="boardNum === 1 && !showSelection">
              <Box @click.once="toNextScreen" id="עילי" class="box btn" :class="{fadeObject: chosenCrane !== ''}"  newTitle="עילי" partBox="0"></Box>
              <!-- <img src="../assets/media/disableBox.svg" class="box disabled" :class="{fadeObject: chosenCrane !== ''}" alt="disableBox"/> -->
              <Box id="disable" class="box btn" :class="{fadeObject: chosenCrane !== ''}" newTitle="disable" partBox="-1"></Box>
               <!-- <Box @click.once="toNextScreen" id="העמסה עצמית" class="box btn" :class="{fadeObject: chosenCrane !== ''}" newTitle="העמסה עצמית"></Box>  -->
            
            </div>
        
            <div class="home-box-container"  v-if="boardNum === 3 || showSelection">
              <Box @click="toStudy(0)" class="part-one btn" newTitle="תחילת הלמידה" partBox="1" id=""></Box>
              <Box @click="toStudy(1)" class="part-two btn" newTitle="תפעול" partBox="1"></Box>
              <Box @click="toStudy(2)" class="part-three btn" newTitle="תרגול" partBox="1"></Box>
            </div>
            
           
        </div>
        <div class="ground"></div>
    </div>
</template>

<script>
import Box from '../../src/components/Box.vue';
import HangingBoard from './HangingBoard.vue';

export default {
        name: "open-page",
        components: {Box, HangingBoard},
        props: ["showSelection"],
        data() {
            return {
              infoObject: {
                    "מפתחת לומדה:": 'רב"ט דני שריקי',
                    "גרפיקאית:": 'רב"ט קריסטינה ברחטוב, רב"ט דני שריקי',
                    "מומחה תוכן:": 'רס"ר יוחאי עזרא',
                    'רמ"ד טי"ל:': 'רס"מ שלומי אוגרן',
                    "גרסה:": "ינואר 2025"
                },
                isOpenInfo: false,
                chosenCrane: '',
                showExplain: false,
                boardNum: 1,
                isUp: false,
                isDown: false,
                indexYellowSign: 0,
                fChosen: true,
            };
          },
        methods: {
          showInfo() {
            this.isOpenInfo = true;
          },
          hideInfo() {
            this.isOpenInfo = false;
          },
          toNextScreen(event) {
            if(this.boardNum === 1) {
              this.chosenCrane = event.currentTarget.id;
              this.$emit('theChosenCourse', this.chosenCrane);
              this.indexYellowSign++;
            }
            this.isUp = true;
            let timerdown = setTimeout(()=> {
              this.isDown= true;
              this.boardNum++;
              clearTimeout(timerdown);
            }, 800);
            let timer = setTimeout(()=> {
              this.isUp = false;
              this.isDown = false;
              clearTimeout(timer);
            }, 1500);
            
          },
          toStudy(part) {
            this.$emit('to-study', this.fChosen, part);
            console.log(part);
            if(this.fChosen) {
              this.fChosen = true;
            }
          },

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
}

.btn {
    cursor: pointer;
    pointer-events: visiblePainted;
}

.box {
  z-index: 1;
  position: relative;
}

.disabled {
 height: 90%;
 /* width: 100%; */
 padding-bottom:1rem;
}



.box-container {
  width: 100vw;
  height: 50vh;
  display:flex;
  z-index: 1;
  justify-content: space-evenly;
  align-items: center;
}

.home-box-container {
  width: 20rem;
  height: 80rem;
    display: flex;
    z-index: 1;
    position: relative;
    align-items: center;
    flex-direction: column;
    animation: fadeIn 0.2s linear forwards;
    margin-bottom: 1rem;
    justify-content: center;
}

.part-one {
  position: relative;
  z-index:4;
  margin-left: 2rem;
}

.part-two {
  position: relative;
  z-index: 3;
  margin-top: -4rem;
  margin-left: -3rem;
}

.part-three {
  position: relative;
  z-index: 2;
  margin-top: -4rem;
  /* margin-bottom: 2rem; */
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
  z-index: 2;
}

.info-btn:hover {
    animation: changeColor 0.2s linear forwards;
  }

  @keyframes changeColor {
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
  z-index: 80;
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
  /* z-index: 30; */
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
    z-index: 0;
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

@media screen and (max-width:700px){
  .ground {
    height: 15rem;
  }

.box {
    width: 20rem;
    z-index: 1;
    margin-bottom: 0rem;
  }
  .box-container {
    margin-bottom: 5rem;
  }
}


  .fadeObject {
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

  @keyframes fadeIn {
    0% {
        opacity: 0;
      }
      100% {
        opacity: 1;
      }
  }
</style>