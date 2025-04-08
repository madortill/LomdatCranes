<template>
  <div id="origin-crane-name" :style="{'--bg-color': info.color}">
    <div class="info">
      <p class="header">למה נקרא כך?</p>
      <p>{{ info.text }}</p>
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
      switch (this.craneKind) {
        case "עגורן גשר":
          let crane1 = {
            text: "העגורן נקרא עגורן גשר מפני שקורתו העליונה נעה כגשר מעל המטען.",
            url: "/media/cards/expand/overheadCrane.svg",
            color:'#C8A47C',
          };
          return crane1;
        case "עגורן שער":
          let crane2 = {
            text: "עגורן שער נקרא בשמו מכיוון שהוא נע כשער מעל המטען.",
            url: "/media/cards/expand/gateCrane.svg",
            color: '#6F97BA',
          };
          return crane2;
        case "עגורן עמוד":
          let crane3 = {
            text: "העגורן נקרא עגורן עמוד מפני שקורתו העליונה מחוברת לעמוד וניתן לצודד את הקורה.",
            url: "/media/cards/expand/columnCrane.svg",
            color: '#BADDF4',
          };
          return crane3;
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
  /* height: 25rem; */
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* border:3px solid red; */

}

.info {
  /* height: 100%; */
  width: 40%;
  z-index: 2;
  position: absolute;
  top: 2rem;
  right: 1rem;
}

.the-img {
  width: 44.5vw;
  /* height: 25rem; */
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
}

}
</style>
