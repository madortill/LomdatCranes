<template>
  <div :class="`item level${level}`">
    {{ id }}
  </div>
</template>

<script>
export default {
  name: "crane-card",
  props: ['id', 'level'],
};
</script>

<style scoped>
.item {
  text-align: center;
  color: white;
  font-size: 3rem;
  position: absolute;
  transition: height 1s, width 1s, left 1s, margin-top 1s, line-height 1s, background-color 1s;
}

/* Styles for the different levels */
.level-2 {
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
}

.level0 {
  height: 12rem;
  width: 10rem;
  background-color: #6796e5;
  left: 50%;
}

.level1 {
  height: 10rem;
  width: 8rem;
  background-color: #4ec9e1;
  left: 70%;
}

.level2 {
  height: 7rem;
  width: 5rem;
  background-color: #228291;
  left: 90%;
}

/* Transition */
.level0, .level1, .level2 {
  transition: transform 0.5s, opacity 0.5s;
}
</style>
