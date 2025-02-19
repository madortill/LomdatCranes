<template>
  <div id="box">
    <img src="../../src/assets/media/box.svg" alt="box" class="the-box">
      <p class="text">{{ newTitle }}</p>
  </div>
</template>

<script>
export default {
  name: "box",
  props: ["newTitle"],
  data() {
    return {};
  },
};
</script>

<style scoped>

#box {
  position: relative;
  width: 100%;
}

.text {
  color: #013047;
  font-size: 1.5rem;
  font-weight: bolder;
  width: 7rem;
  transform: rotate(22.13deg);
  position: absolute;
  bottom: 1rem;
  left: 1rem;
}

.the-box {
  width: 100%;
  height: 100%;
}
</style>
