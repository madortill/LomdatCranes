<template>
    <div id="clouds-btns">
        <img v-for="num in numbers" :key="num" :class="`cloud${num}`" :src="getCloudImage(num)" alt="cloud image" />
        <p v-for="(title,index) in arrTitles"  :key="index">{{arrTitles[index]}}</p>
    </div>
</template>

<script>
export default {
  name: "clouds-btns",
  data() {
    return {
        numbers: [1, 2, 3, 4, 5], // List of numbers to dynamically generate image sources
        arrTitles: ['ידית פיקוד תלויה ומקובעת על הקורה', 'פיקוד ע"י שלט אלחוטי', 'ידית פיקוד ניידת לאורך הקורה', 'ידית פיקוד תלויה על הכננת', 'פיקוד מתוך תא'],
    };
  },
  methods: {
    getCloudImage(num) {
      // Determine the base URL (for local and production)
      const basePath = process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return `${basePath}media/clouds/SVG/cloud${num}.svg`;  // Static path to the images in the public folder
    }
  },
  computed: {
   
  } 
}; 
</script>

<style scoped>
  #clouds-btns {
    position: absolute;
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: 10% 10% 10% 10% 10% 10% 10% 10% 10% 10%;
    grid-template-rows: 10% 10% 10% 10% 10% 10% 10% 10% 10% 10%;
    align-items: center;
    overflow: hidden;
    /* background-color: #e0f2f4; */
  }
 /* Cloud 1 */
 .cloud1 {
    width: 21rem;
    grid-column-start: 4;
    grid-row-start: 3;
    /* animation: moveClouds 20s linear infinite; Move cloud1 */
  }
  
  /* Cloud 2 */
  .cloud2 {
    width: 19rem;
    grid-column-start: 2;
    grid-row-start: 6;
    /* animation: moveClouds 25s linear infinite; Move cloud2 */
  }
  
  /* Cloud 3 */
  .cloud3 {
    width: 16rem;
    grid-column-start: 7;
    grid-row-start: 4;
    /* animation: moveClouds 30s linear infinite; Move cloud3 */
  }
  
  /* Cloud 4 */
  .cloud4 {
    width: 18rem;
    grid-column-start: 8;
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

  @media screen and (max-width: 600px) {
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

