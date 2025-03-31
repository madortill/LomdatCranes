<template>
  <div id="types-of-cranes">
    <p class="header">{{ title }}</p>

    <crane-carousel :style="{ display: !cardClicked ? 'block' : 'none' }" @change-title="changeTitle" />
    <origin-crane-name :style="{ display: cardClicked ? 'flex' : 'none' }" :craneKind="clickedCrane"></origin-crane-name>
  </div>
</template>

<script>
import CraneCarousel from "./CraneCarousel.vue";
import OriginCraneName from './OriginCraneName.vue';

export default {
  components: { CraneCarousel , OriginCraneName },
  name: "types-of-cranes",
  props: ['cardClicked', 'title'],
  data() {
    return {
      clickedCrane: '',

    };
  },
  methods: {
    changeTitle(craneTitle) {
      this.clickedCrane = craneTitle;
      this.$emit('crane-card-chosen', craneTitle);
    },
  },
};
</script>

<style scoped>
#types-of-cranes {
  width: 100vw;
  height: 77vh;
  margin-top: 5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
  /* padding: 2rem; */
}
@media screen and (max-width: 700px) {
}
</style>
