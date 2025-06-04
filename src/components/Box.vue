<template>
  <div id="box">
    <img  v-if="newTitle === 'disable-start'" alt="box" class="the-box" src="/media/startDisableBox.svg"/>
    <img v-if="newTitle !== 'disable-start'" :src="imageSource" alt="box" class="the-box" />
    <p v-if="newTitle !== 'disable-start'" class="text" :class="partBox === '0' ? 'startPos' : 'homePos'">{{ newTitle }}</p>
  </div>
</template>

<script>
export default {
  name: "box",
  props: ["newTitle", "partBox", "isDisable"],
  data() {
    return {};
  },
  computed: {
    // Dynamically return the src based on the condition
    imageSource() {
      const basePath = process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return this.isDisable === true ?  `${basePath}media/disableBox.svg` : `${basePath}media/box.svg`;
    },
    
  },
};
</script>

<style scoped>
#box {
  position: relative;
  width: 13rem;
}

.text {
  color: #013047;
  font-size: 1.5rem;
  font-weight: bolder;
  width: 7rem;
  transform: rotate(22.13deg);
  position: absolute;
}

.startPos {
  bottom: 3rem;
  left: 0.5rem;
}

.homePos {
  bottom: 1rem;
  left: 0rem;
}

.the-box {
  width: 13rem;
}
</style>
