<template>
  <div id="clouds-bg">
    <img v-for="num in numbers" :key="num" :class="`cloud${num}`" :src="getCloudImage(num)" alt="cloud image" />
  </div>
</template>

<script>
export default {
  name: "clouds-bg",
  data() {
    return {
      numbers: [1, 2, 3, 4, 5] // List of numbers to dynamically generate image sources
    };
  },
  methods: {
    getCloudImage(num) {
      // Determine the base URL (for local and production)
      const basePath = process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return `${basePath}/src/assets/media/clouds/cloud${num}.png`;  // Static path to the images in the public folder
    }
  }
};
</script>


  
  <style scoped>
  #clouds-bg {
    position: absolute;
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: 20% 20% 20% 20% 20%;
    grid-template-rows: 20% 20% 20% 20% 20%;
    align-items: center;
    overflow: hidden;
  }
  
  /* Define the animation to move clouds from right to left */
  @keyframes moveClouds {
    0% {
      transform: translateX(100%); /* Start from the right (off-screen) */
      opacity: 0;
    }
    10% {
        opacity: 1;
    }
    90%{
        opacity: 1;
    }
    100% {
      transform: translateX(-100%); /* Move to the left (off-screen) */
      opacity: 0;
    }
  }
  
  /* Cloud 1 */
  .cloud1 {
    width: 10rem;
    grid-column-start: 4;
    grid-row-start: 1;
    animation: moveClouds 20s linear infinite; /* Move cloud1 */
  }
  
  /* Cloud 2 */
  .cloud2 {
    width: 10rem;
    grid-column-start: 2;
    grid-row-start: 2;
    animation: moveClouds 25s linear infinite; /* Move cloud2 */
  }
  
  /* Cloud 3 */
  .cloud3 {
    width: 6rem;
    grid-column-start: 5;
    grid-row-start: 3;
    animation: moveClouds 30s linear infinite; /* Move cloud3 */
  }
  
  /* Cloud 4 */
  .cloud4 {
    width: 6rem;
    grid-column-start: 3;
    grid-row-start: 4;
    animation: moveClouds 33s linear infinite; /* Move cloud4 */
  }
  
  /* Cloud 5 */
  .cloud5 {
    width: 10rem;
    grid-column-start: 1;
    grid-row-start: 5;
    animation: moveClouds 40s linear infinite; /* Move cloud5 */
  }
  </style>
  