<template>
  <div id="instruction-container">
    <p class="instruction main-instruction">
      {{ instructionsArr[numInstruction] }}
    </p>
    <p class="instruction sub-instruction">-{{ addition }} בלחיצה -</p>
  </div>
</template>

<script>
export default {
  name: "instruction",
  props: ["numInstruction"],
  data() {
    return {
      instructionsArr: [
        "יש לפתוח את ארון החשמל",
        "נא לפתוח את כפתור הזרם הראשי",
        "נא לפתוח את קופסת האחסון",
        "נא להוציא את השלט",
        "נא לשחרר את פטריית החירום",
        "נא לשחרר את העגורן ממקום האחסון שלו",
      ],
      addition: "",
    };
  },
  methods: {},
};
</script>

<style scoped>
#instruction-container {
  background-color: white;
  width: 30rem;
  height: 8rem;
  border-radius: 1rem;
  margin-top: 3.5rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

.instruction {
  margin: 0rem;
}

.sub-instruction {
  margin-bottom: 1rem;
}

.main-instruction {
  font-size: 1.3rem;
  font-weight: bold;
}

@media screen and (max-width: 600px) {
  #instruction-container {
    width: 26rem;
    height: 7rem;
  }
}
</style>
