<template>
  <div id="info-screen">
    <navbar :part="navPart" :subjNum="subNavPart"></navbar>
    <info-hanging-board :section="infoHangingPart" :chosenCourse="chosenCourse" :flipStart="flipStart" :flipEndDefine="flipEndDefine" :backFlip="backFlip" :flipEndSaftyRules="flipEndSaftyRules"></info-hanging-board>
    <p class="next-btn moving-btn" id="next" @click="nextPart">הבא</p>
    <p class="back-btn moving-btn" id="back" @click="nextPart">חזור</p>
  </div>
</template>

<script>
import InfoHangingBoard from "./InfoHangingBoard.vue";
import Navbar from "./Navbar.vue";
export default {
  name: "info-screen",
  components: { Navbar, InfoHangingBoard },
  props: ["navPart", "chosenCourse"],
  data() {
    return {
      Infopart: 1,
      infoHangingPart: 0,
      subNavPart: 1,
      flipStart: false,
      flipEndDefine: false,
      backFlip: false,
      flipEndSaftyRules:false,
    };
  },
  methods: {
            nextPart(event) {
                if(event.currentTarget.id === 'next' && this.infoHangingPart === 0) {
                  //to restart values
                  this.flipEndSaftyRules = false;
                  this.backFlip = false;
                  //
                  this.subNavPart++; 
                  this.flipEndDefine = true;
                    let timer = setTimeout(()=> {
                      this.infoHangingPart++;
                      this.flipStart = true;
                      clearTimeout(timer);
                    }, 590);
                    
                } else if (event.currentTarget.id === 'back' && this.infoHangingPart === 1){
                   //to restart values
                   this.flipEndDefine = false;
                  this.flipStart = false;
                  //
                    this.subNavPart--;
                    this.backFlip = true;
                    let timer = setTimeout(()=> {
                      this.infoHangingPart--;
                      this.flipEndSaftyRules = true;
                      clearTimeout(timer);
                    }, 590);
                }
                
            }
        },
};
</script>

<style scoped>
#info-screen {
  z-index: 7;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.moving-btn {
  /* z-index: 1; */
  position: absolute;
  bottom: 1rem;
  width: 5rem;
  height: 3rem;
  font-size: 1rem;
  background-color: #8cd0ec;
  border-radius: 1.5rem;
  padding: 0; /* Remove padding to ensure centering works properly */
  /* Centering the text */
  display: flex;
  justify-content: center; /* Horizontally centers the text */
  align-items: center; /* Vertically centers the text */
  text-align: center; /* Ensures the text is centered if multiline */
  transition: background-color 0.3s ease;
}

.moving-btn:hover {
  background-color: #023047;
  color: white;
}

.next-btn {
    left: 1rem;
}

.back-btn {
    right: 1rem;
}

@media screen and (max-width: 425px) {
  .moving-btn {
    bottom: 3rem;
    width: 7rem;
    height: 5rem;
    font-size: 1.5rem;
    border-radius: 2rem;
  }
}
</style>
