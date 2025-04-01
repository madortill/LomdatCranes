<template>
  <div id="types-of-cranes">
    <p class="header">{{ title }}</p>

    <crane-carousel
      :style="{ display: !cardClicked ? 'block' : 'none' }"
      @change-title="changeTitle"
      :arrLearnedCards="arrLearnedCards"
    />
    <div :style="{ display: cardClicked ? 'block' : 'none' }">
      <origin-crane-name
        v-if="partLearningCraneCard === 0"
        :craneKind="clickedCrane"
      ></origin-crane-name>
      <crane-operations
        v-if="partLearningCraneCard === 1"
        :craneKind="clickedCrane"
      ></crane-operations>
    </div>
  </div>
</template>

<script>
import CraneCarousel from "./CraneCarousel.vue";
import CraneOperations from "./CraneOperations.vue";
import OriginCraneName from "./OriginCraneName.vue";

export default {
  components: { CraneCarousel, OriginCraneName, CraneOperations },
  name: "types-of-cranes",
  props: ["cardClicked", "title", "partLearningCraneCard", "arrLearnedCards"],
  data() {
    return {
      clickedCrane: "",
    };
  },
  methods: {
    changeTitle(craneTitle) {
      this.clickedCrane = craneTitle;
      this.$emit("crane-card-chosen", craneTitle);
    },
  
  },
};
</script>

<style scoped>
#types-of-cranes {
  width: 100vw;
  /* height: 77vh; */
  margin-top: 5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
  /* padding: 2rem; */
}
@media screen and (max-width: 700px) {
  #types-of-cranes {
    margin-top: 5rem;
  }
}
</style>
