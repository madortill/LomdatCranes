<template>
  <div class="potential-additions">
    <div
      v-for="(info, index) in arrInfo"
      :key="index"
      class="bubble"
      :style="{ backgroundColor: arrColors[index] }"
    >
      <p class="the-info">{{ info }}</p>
      <img
        class="fix-pos"
        src="/media/potentialAdditions/whiteBgForBubble.svg"
        alt="whiteBgForBubble"
      />
      <img class="icon" :src="getIconUrl(index)" alt="icon" />
    </div>
  </div>
</template>

<script>
export default {
  name: "potential-additions",
  data() {
    return {
      arrInfo: [
        "מערכת תאורה",
        "צופר אזהרה",
        "גששים וחיישנים למניעת תקלות והגברת בטיחות",
        "מכשיר למדידת משקל מטען",
      ],
      arrColors: ["#F88C01", "#FFAF02", "#8CD0EC", "#1E85AE"],
    };
  },
  methods: {
    getIconUrl(num) {
      // Determine the base URL (for local and production)
      const basePath =
        process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return `${basePath}media/potentialAdditions/icons/icon${num}.png`; // Static path to the images in the public folder
    },
  },
  computed: {},
};
</script>

<style scoped>
.the-info {
  display: flex;
  margin-right: 1rem;
  width: 14rem;
}

.header {
  font-size: 1.8rem;
  text-align: center;
  font-weight: bold;
}

.bubble {
  background-color: white;
  border-radius: 1rem;
  width: 25rem;
  position: relative;
  display: flex;
  margin-bottom: 0.5rem;
  height: 3.7rem;
  align-items: center;
}

.potential-additions {
  height: 18rem;
  margin-top: 1rem;
}

.fix-pos {
  position: absolute;
  top: 0rem;
  left: 0rem;
  height: 105%;
}

.icon {
  z-index: 1;
  position: absolute;
  left: 2rem;
  width: 4rem;
}
</style>
