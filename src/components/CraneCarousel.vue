<template>
  <div id="crane-carousel">
    <div id="carousel" class="noselect">
      <div class="arrow arrow-right" @click="moveRight">R</div>
      <transition-group class="cards-container" name="carousel" tag="div">
        <crane-card
          v-for="(item, index) in items"
          :key="item"
          :id="item"
          :level="getLevel(index)"
        />
      </transition-group>

      <div class="arrow arrow-left" @click="moveLeft">L</div>
    </div>
  </div>
</template>

<script>
import CraneCard from "./CraneCard.vue";

export default {
  components: { CraneCard },
  name: "crane-carousel",
  data() {
    return {
      items: ['עגורן גשר', 'עגורן עמוד', 'עגורן שער'], // List of cards
      active: 0, // Active card
    };
  },
  methods: {
    // Move to the left by shifting the first item
    moveLeft() {
      const firstItem = this.items.shift(); // Remove the first item
      this.items.push(firstItem); // Add it to the end
    },
    // Move to the right by removing the last item
    moveRight() {
      const lastItem = this.items.pop(); // Remove the last item
      this.items.unshift(lastItem); // Add it to the start
    },
    // Get the level of each card based on its position
    getLevel(index) {
      const offset = index - this.active;
      if (offset === 0) return 0; // Center card
      if (offset === 1) return 1; // Right card
      if (offset === -1) return -1; // Left card
      return 2; // Farthest left or right card
    },
  },
};
</script>

<style scoped>
#crane-carousel {
  /* width: 80vw; */
  height: 30rem;
  /* position: relative; */
  /* margin: 0 auto; */
  overflow: hidden; /* Hide overflow */
  display: flex;
}

.arrow {
  /* position: absolute; */
  width: 3rem;
  height: 3rem;
  background-color: white;
  text-align: center;
  font-size: 2rem;
  border-radius: 50%;
  cursor: pointer;
  color: #228291;
  /* line-height: 30px; */
  /* margin-top: 85px; */
  /* z-index: 1000; */
}

/* .arrow-left {
  left: 1rem;
}

.arrow-right {
  right: 1rem;
} */

.noselect {
  /* -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none; */
  display: flex;
  align-items: center;
}

.cards-container {
  width: 60rem;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

/* Transition Classes */
.carousel-enter-active,
.carousel-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.carousel-enter,
.carousel-leave-to {
  opacity: 0;
  transform: translateX(100px);
}

.carousel-enter-to,
.carousel-leave {
  opacity: 1;
  transform: translateX(0);
}
</style>
