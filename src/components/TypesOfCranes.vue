<template>
  <div id="types-of-cranes">
    <p class="header">{{ titlesArray[titleIndex] }}</p>
  </div>
</template>

<script>
export default {
  name: "types-of-cranes",
  data() {
    return {
      titlesArray: [
        "סוגי העגורנים הקיימים",
        "עגורן שער",
        "עגורן עמוד",
        "עגורן גשר",
      ],
      titleIndex: 0,
    };
  },
  methods: {},
};
</script>

<style scoped>
#types-of-cranes {
    width: 100vw;
    height: 70vh;
    margin-top: 5rem;
  /* display: flex;
  justify-content: center;
  color: white;
  align-items: flex-end; */
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
}
@media screen and (max-width: 700px) {
}
</style>
