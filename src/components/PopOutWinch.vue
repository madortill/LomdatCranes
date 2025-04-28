<template>
  <div :class="'part-' + part" id="pop-out-winch">
    <p @click="closeWindow" class="close-info"  v-if="!((indexTypes === 2 || indexTypes === 3) && !showCloseBtn)">X</p>

    <p class="header">{{ title }}</p>
    <p>{{ explainArr[part][indexTypes] }}</p>
    <p class="instraction" v-if="part === 1">- לחצו על הכרטיסיות -</p>

    <container-part-winch
      :indexInfoArr="indexInContainerPartWinch"
      v-if="part === 1"
      @finish-learning="toShowCloseBtn"
    ></container-part-winch>

    <button @click="prevPart" v-if="showBackBtn" class="moving-btn back-btn">
      חזור
    </button>
    <button
      @click="nextPart"
      v-if="(indexTypes === 2 || indexTypes === 3) && showNextBtn"
      class="moving-btn next-btn"
    >
      הבא
    </button>
  </div>
</template>

<script>
import ContainerPartWinch from "./ContainerPartWinch.vue";
export default {
  components: { ContainerPartWinch },
  name: "pop-out-winch",
  props: ["title", "indexTypes"],
  data() {
    return {
      explainArr: [
        [
          "מופעלת באופן מכאני ומיועדת לכבל לב חבל",
          "מופעלת באופן מכאני ומיועדת לשרשרת הרמה",
          "מופעלת באמצעות מנוע חשמלי המיועד לשרשרת הרמה",
          "מופעלת באמצעות מנוע חשמלי המיועד לכבל לב חבל",
        ],
        [
          "",
          "",
          "ישנם מספר חלקים לכננת הרמה לשרשרת:",
          "ישנם מספר חלקים בכננת החשמלית:",
        ],
      ],
      showNextBtn: true,
      showBackBtn: false,
      showCloseBtn: false,
      part: 0,
      indexInContainerPartWinch: 0,
      colorCardsArr: [
        ["#F88C01", "#FFAF02", "#8CD0EC", "#1E85AE"],
        ["#F88C01", "#FFAF02", "#FFD169", "#8CD0EC", "#1E85AE"],
      ],
    };
  },
  methods: {
    closeWindow() {
      this.$emit("close-pop-out");
      this.showCloseBtn = false;
      //check if finish learn btn
      if (this.indexTypes === 0 || this.indexTypes === 1) {
        // this.finishLearning();
        this.$emit("finish-learning", this.indexTypes);

      }
    },
    nextPart() {
      this.showNextBtn = false;
      this.showBackBtn = true;
      this.part++;
      if (this.indexTypes === 3) {
        this.indexInContainerPartWinch = 1;
      } else {
        this.indexInContainerPartWinch = 0;
      }
    },
    prevPart() {
      this.showNextBtn = true;
      this.showBackBtn = false;
      this.part--;
    },
    //it will show if the user finished learning all the parts
    toShowCloseBtn() {
      this.showCloseBtn = true;
      this.$emit("finish-learning", this.indexTypes);
    },
  },
  computed: {},
};
</script>

<style scoped>
#pop-out-winch {
  /* background-color: #023047; */
  background-color: white;
  /* padding: 1rem; */
  border-radius: 1rem;
  position: absolute;
  /* color: white; */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: height 0.3s ease, width 0.3s ease;
}

.part-0 {
  height: 20rem;
  width: 30rem;
}

.part-1 {
  height: 28rem;
  width: 33rem;
}
.header {
  font-size: 2rem;
  font-weight: bold;
  /* padding: 2rem; */
}

.close-info {
  /* margin-left: 22rem; */
  cursor: pointer;
  font-size: 1.8rem;
  position: absolute;
  right: 1rem;
  top: -1rem;
  /* z-index: 30; */
}

.moving-btn {
  z-index: 1;
  position: absolute;
  bottom: 1rem;
  width: 4rem;
  height: 2rem;
  font-size: 1rem;
  background-color: #8cd0ec;
  border: none;
  border-radius: 1.5rem;
  padding: 0; /* Remove padding to ensure centering works properly */
  /* Centering the text */
  display: flex;
  justify-content: center; /* Horizontally centers the text */
  align-items: center; /* Vertically centers the text */
  text-align: center; /* Ensures the text is centered if multiline */
  transition: background-color 0.3s ease;
  color: black;
  cursor: pointer;
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

.instraction {
  font-size: 0.8rem;
  margin-top: -0.8rem;
  font-weight: bold;
}


@media screen and (max-width: 700px) {
  .part-0 {
  width: 28rem;
}

.part-1 {
  height: 27.5rem;
  width: 30rem;
}

.part-of-winch {
  width: 5.6rem;
}

.header {
    margin-bottom: 0.5rem;
}

.height-after-click{
    height: 13rem;
}
}
</style>
