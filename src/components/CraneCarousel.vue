<template>
  <div id="crane-carousel">
    <div id="carousel" class="noselect">
      <div class="arrow for-computer" @click="moveRight">
        {{ arrArrows[1] }}
      </div>
      <transition-group class="cards-container" name="carousel" tag="div">
        <crane-card
          v-for="(item, index) in items"
          :key="item"
          :id="item"
          :level="getLevel(index)"
          @click="showCard($event, item)"
          :style=" this.arrLearnedCards.includes(item) ? 'filter: grayscale(100%)' : ''"
        />
      </transition-group>

      <div class="arrow for-computer" @click="moveLeft">{{ arrArrows[0] }}</div>
      <div class="arrow-phone-container">
        <div class="arrow" @click="moveRight">
          {{ arrArrows[1] }}
        </div>
        <div class="arrow" @click="moveLeft">
          {{ arrArrows[0] }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CraneCard from "./CraneCard.vue";

export default {
  components: { CraneCard },
  props: ['arrLearnedCards'],
  name: "crane-carousel",
  // props: ["learnedCardsArr"],
  data() {
    return {
      items: ["עגורן גשר", "עגורן עמוד", "עגורן שער"], // List of cards
      active: 0, // Active card
      arrArrows: [">", "<"],
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
    showCard(event, title) {
      //disable if the card not in the center
      if (event.target.classList.contains("level1")) {
        this.$emit("change-title", title);
      }
    },
   
  }, 
};
</script>

<style scoped>
#crane-carousel {
  width: 80vw;
  height: 30rem;
  overflow: hidden; /* Hide overflow */
  display: flex;
  justify-content: center;
}

.arrow {
  width: 3rem;
  height: 3rem;
  background-color: white;
  text-align: center;
  font-size: 2rem;
  border-radius: 50%;
  cursor: pointer;
  color: #228291;
  display: flex;
  align-items: center;
  justify-content: center;
}

.arrow-phone-container {
  display: none;
  position: absolute;
  width: 12rem;
  bottom: 10rem;
  justify-content: space-evenly;
}
.noselect {
  display: flex;
  align-items: center;
  justify-content: center;
}

.cards-container {
  width: 50rem;
  height: 30rem;
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

@media screen and (max-width: 600px) {
  .cards-container {
    width: 76rem;
  }

  /* #crane-carousel {
    width: 30rem;
    } */

  .for-computer {
    display: none;
  }

  .arrow-phone-container {
    display: flex;
  }

  .arrow {
    width: 4rem;
    height: 3rem;
  }
}
</style>
