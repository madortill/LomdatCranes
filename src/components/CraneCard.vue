<template>
  <div  tabindex="0" :class="`item level${level}`"  >
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
  transition: height 1s, width 1s, left 1s, margin-top 1s, line-height 1s, background-color 1s;
}

.img-card {
  width:100%;
  height:100%;
}

.level0 {
  height: 16rem;
  width: 10rem;

}

.level1 {
  height: 20rem;
  width: 14rem;
  cursor: pointer;
  transition: all 0.5s ease; /* תנועה חלקה */
}

.level1:hover{
  transform: scale(1.05);
  box-shadow: 0 0 1rem 1rem white; 
}

.level1:focus{
  transform: scale(1.3);
  z-index: 4;
}

.level2 {
  height: 16rem;
  width: 10rem;
}

/* Transition */
.level0, .level1, .level2 {
  transition: transform 0.5s, opacity 0.5s;
}

@media screen and (max-width: 600px) {
.level1 {
  height: 16rem;
  width: 11.1rem; 
  box-shadow: 0 0 1rem 1rem white; 
}

.level2, .level0 {
  height: 14rem;
  width: 8rem;
}
}
</style>
