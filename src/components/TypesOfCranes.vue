<template>
  <div id="types-of-cranes">
    <p class="header">{{ title }}</p>

    <crane-carousel :style="{ display: !cardClicked ? 'block' : 'none' }" @change-title="changeTitle" />
  </div>
</template>

<script>
import CraneCarousel from "./CraneCarousel.vue";

export default {
  components: { CraneCarousel },
  name: "types-of-cranes",
  props: ['cardClicked', 'title'],
  data() {
    return {
    

    };
  },
  methods: {
    changeTitle(craneTitle) {
      this.$emit('crane-card-chosen', craneTitle);
    },
  },
};
</script>

<style scoped>
#types-of-cranes {
  width: 100vw;
  height: 70vh;
  margin-top: 5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
}
@media screen and (max-width: 700px) {
}
</style>
