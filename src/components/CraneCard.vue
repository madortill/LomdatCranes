<template>
  <div :class="`item level${level}`"  >
    <img :class="`img-card num${level}`" :src="srcCard" alt="card" />  
  </div>
</template>

<script>
export default {
  name: "crane-card",
  props: ['id', 'level', 'srcCard'],
};
</script>

<style scoped>
.item {
  text-align: center;
  color: white;
 border-radius: 1.4rem;
 /* padding: 1rem; */
  transition: height 1s, width 1s, left 1s, margin-top 1s, line-height 1s, background-color 1s;
  /* background-size: 200%;
  background-repeat: no-repeat; 
  background-position: center;   */
}

.img-card {
  width:100%;
  height:100%;
}
/* Styles for the different levels */
/* .level-2 {
  height: 7rem;
  width: 5rem;
  background-color: #228291;
  left: 10%;
}

.level-1 {
  height: 10rem;
  width: 8rem;
  background-color: #4ec9e1;
  left: 30%;
} */

.level0 {
  height: 16rem;
  width: 10rem;
  /* background-color: #4ec9e1; */
  /* font-size: 2rem; */
}

.level1 {
  height: 20rem;
  width: 14rem;
  /* background-color: #4ec9e1;
  font-size: 3rem; */
  cursor: pointer;
  transition: all 0.5s ease; /* תנועה חלקה */
}

.level1:hover{
  transform: scale(1.05);
  box-shadow: 0 0 1rem 1rem white; 
}

.level2 {
  height: 16rem;
  width: 10rem;
  /* background-color: #4ec9e1;
  font-size: 2rem; */
}

/* Transition */
.level0, .level1, .level2 {
  transition: transform 0.5s, opacity 0.5s;
}

@media screen and (max-width: 600px) {
.level1 {
  height: 16rem;
  width: 13rem;
  /* transform: scale(1.05); */
  box-shadow: 0 0 1rem 1rem white; 
}

.level2, .level0 {
  height: 14rem;
  width: 8rem;
}
}
</style>
