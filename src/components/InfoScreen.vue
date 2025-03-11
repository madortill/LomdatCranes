<template>
  <div id="info-screen">
    <navbar :part="navPart"></navbar>
    <info-hanging-board :section="infoHangingPart" :chosenCourse="chosenCourse"></info-hanging-board>
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
    };
  },
  methods: {
            nextPart(event) {
                if(event.currentTarget.id === 'next' && this.infoHangingPart === 0) {
                    this.infoHangingPart++;
                } else if (event.currentTarget.id === 'back' && this.infoHangingPart === 1){
                    this.infoHangingPart--;
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
</style>
