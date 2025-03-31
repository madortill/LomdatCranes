<template>
    <div id="origin-crane-name">
      <div class="info">
        <p class="header">למה נקרא כך?</p>
        <p>{{ info }}</p>
      </div>
      <div class="animation">animation</div>
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
            return "העגורן נקרא עגורן גשר מפני שקורתו העליונה נעה כגשר מעל המטען.";
          case "עגורן שער":
            return "עגורן שער נקרא בשמו מכיוון שהוא נע כשער מעל המטען.";
          case "עגורן עמוד":
            return "העגורן נקרא עגורן עמוד מפני שקורתו העליונה מחוברת לעמוד וניתן לצודד את הקורה.";
          default:
            return "מידע לא זמין.";
        }
      },
    },
  };
  </script>
  
  <style scoped>
  #origin-crane-name {
    display: flex;
    margin-top: 1rem;
    background-color: white;
    border-radius: 1rem;
    width: 55vw;
    height: 30rem;
    align-items: center;
    justify-content: space-between;
  }
  
  .info {
    height: 100%;
    width: 40%;
  }
  
  .header {
    font-size: 1.8rem;
    text-align: center;
    font-weight: bold;
  }
  </style>
  