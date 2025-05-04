<template>
  <div id="clouds-btns">
    <p class="header">שיטות פיקוד</p>
    <p v-if="!inPopOut" class="fix-pos">
      ישנם מספר דרכים לשלוט בפעילות העגורן:
    </p>
    <div v-if="!inPopOut" class="clouds-btns-container">
      <div
        v-for="(num, index) in numbers"
        :key="index"
        :class="[`cloud${num}`, !learnedArr[num] ? 'flying' : '']"
        class="cloud-container"
       
      >
        <img  @click="inTheMethod(true, index, $event)" class="img-cloud" :src="getCloudImage(num)" alt="cloud image" />
        <p
          :class="num === 1 || num === 4 || num === 5 ? 'title' + num : ''"
          class="title"
        >
          {{ arrTitles[index] }}
        </p>
      </div>
    </div>
    <command-method
      v-if="inPopOut"
      @finished-method="inTheMethod"
      :cloudObject="chosenMethod"
    ></command-method>
  </div>
</template>

<script>
import CommandMethod from "./CommandMethod.vue";
export default {
  name: "clouds-btns",
  components: { CommandMethod },
  data() {
    return {
      numbers: [1, 2, 3, 4, 5], // List of numbers to dynamically generate image sources
      arrTitles: [
        "ידית פיקוד תלויה ומקובעת על הקורה",
        'פיקוד ע"י שלט אלחוטי',
        "ידית פיקוד ניידת לאורך הקורה",
        "ידית פיקוד תלויה על הכננת",
        "פיקוד מתוך תא",
      ],
      learnedArr: [false, false, false, false, false],
      inPopOut: false,
      chosenMethod: { src: "", text: "" },
    };
  },
  methods: {
    getCloudImage(num) {
      // Determine the base URL (for local and production)
      const basePath =
        process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return `${basePath}media/clouds/SVG/cloud${num}.svg`; // Static path to the images in the public folder
    },

    inTheMethod(isIn, index, event) {
      this.inPopOut = isIn;
      if (isIn) {
        this.learnedArr[index+1] = true;
        this.chosenMethod.src = event.currentTarget.src;
        this.chosenMethod.text = this.arrTitles[index];
      }
    },
  },
  computed: {},
};
</script>

<style scoped>
#clouds-btns {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 6rem;
}
.clouds-btns-container {
  /* position: absolute; */
  width: 100%;
  height: 71%;
  display: grid;
  grid-template-columns: 10% 10% 10% 10% 10% 10% 10% 10% 10% 10%;
  grid-template-rows: 10% 10% 10% 10% 10% 10% 10% 10% 10% 10%;
  align-items: center;
  overflow: hidden;
  /* background-color: #e0f2f4; */
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
}

.fix-pos {
  margin-top: -1rem;
}
.img-cloud {
  position: absolute;
  width: 100%;
  /* height: 100%; */
  right: 0rem;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  /* z-index: 1; */
}

@keyframes flyingUpDown {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px); /* Move up */
  }
  100% {
    transform: translateY(0);
  }
}

.flying {
  animation: flyingUpDown 2.5s ease-in-out infinite;
}
.title {
  z-index: 2;
  position: relative;
  width: 11rem;
  margin-top: 3rem;
  pointer-events: none;
}

.title1 {
  margin-left: 4rem;
}

.title4 {
  margin-right: 2rem;
}

.title5 {
  margin-right: 4rem;
}

.cloud-container {
  position: relative;
  height: 10rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Cloud 1 */
.cloud1 {
  width: 21rem;
  grid-column-start: 3;
  grid-row-start: 2;
}

/* Cloud 2 */
.cloud2 {
  width: 19rem;
  grid-column-start: 2;
  grid-row-start: 5;
}

/* Cloud 3 */
.cloud3 {
  width: 16rem;
  grid-column-start: 7;
  grid-row-start: 3;
}

/* Cloud 4 */
.cloud4 {
  width: 18rem;
  grid-column-start: 8;
  grid-row-start: 6;
}

/* Cloud 5 */
.cloud5 {
  width: 24rem;
  grid-column-start: 3;
  grid-row-start: 8;
}

@media screen and (max-width: 600px) {
  .clouds-btns-container {
    position: absolute;
    bottom: 6rem;
  }

  /* Cloud 1 */
  .cloud1 {
    width: 21rem;
    grid-column-start: 4;
    grid-row-start: 2;
    /* animation: moveClouds 20s linear infinite; Move cloud1 */
  }

  /* Cloud 2 */
  .cloud2 {
    width: 19rem;
    grid-column-start: 1;
    grid-row-start: 5;
    /* animation: moveClouds 25s linear infinite; Move cloud2 */
  }

  /* Cloud 3 */
  .cloud3 {
    width: 16rem;
    grid-column-start: 6;
    grid-row-start: 4;
    /* animation: moveClouds 30s linear infinite; Move cloud3 */
  }

  /* Cloud 4 */
  .cloud4 {
    width: 18rem;
    grid-column-start: 3;
    grid-row-start: 7;
    /* animation: moveClouds 33s linear infinite; Move cloud4 */
  }

  /* Cloud 5 */
  .cloud5 {
    width: 24rem;
    grid-column-start: 3;
    grid-row-start: 9;
    /* animation: moveClouds 40s linear infinite; Move cloud5 */
  }
}
</style>
