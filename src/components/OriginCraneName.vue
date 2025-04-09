<template>
  <div id="origin-crane-name" :style="{'--bg-color': info.color}">
    <div class="info">
      <p class="header">למה נקרא כך?</p>
      <p class="the-text">{{ info.text }}</p>
    </div>
    <div class="blue-void-phone"></div>
    <img class="the-img" :src="info.url" />
  </div>
</template>

<script>
export default {
  name: "origin-crane-name",
  props: ["craneKind"],
  computed: {
    info() {
      const baseUrl = import.meta.env.BASE_URL; // Get the correct base URL
      switch (this.craneKind) {
        case "עגורן גשר":
          return {
            text: "העגורן נקרא עגורן גשר מפני שקורתו העליונה נעה כגשר מעל המטען.",
            url: `${baseUrl}media/cards/expand/overheadCrane.svg`, // Use BASE_URL here
            color: '#C3996D',
          };
        case "עגורן שער":
          return {
            text: "עגורן שער נקרא בשמו מכיוון שהוא נע כשער מעל המטען.",
            url: `${baseUrl}media/cards/expand/gateCrane.svg`,
            color: '#5F8BB3',
          };
        case "עגורן עמוד":
          return {
            text: "העגורן נקרא עגורן עמוד מפני שקורתו העליונה מחוברת לעמוד וניתן לצודד את הקורה.",
            url: `${baseUrl}media/cards/expand/columnCrane.svg`,
            color: '#B3DAF4',
          };
        default:
          return "מידע לא זמין.";
      }
    },
  },
};
</script>

<style scoped>
#origin-crane-name {
  margin-top: 1rem;
  width: 44.5vw;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.info {
  width: 40%;
  z-index: 2;
  position: absolute;
  top: 2rem;
  right: 1rem;
}

.the-img {
  width: 44.5vw;
  z-index: 0;
}



.header {
  font-size: 1.8rem;
  text-align: center;
  font-weight: bold;
}

@media screen and (max-width: 600px) {
  #origin-crane-name {
    flex-direction: column;
    width: 72.5vw;
  }

  .the-img {
    width: 72.5vw;
}
}

@media screen and (max-width: 880px) {

#origin-crane-name {
  /* background-color: var(--bg-color); */
  border-radius: 2rem;
}

.info {
    width: 90%;
    position: static;
    height: 18rem;
    background-color: var(--bg-color);
    width: 100%;
  }

  .the-img {
    margin-top: -1rem;
    z-index: 2;
}

.the-text {
  padding: 1rem;
}
}
</style>
