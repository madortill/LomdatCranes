<template>
  <div id="crane-operations">
    <p class="header">פעולות העגורן</p>
    <div class="bubble-container">
      <div v-for="(info, index) in arrinfo" :key="index" class="bubble">
        {{ info }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "crane-operations",
  props: ["craneKind"],
  computed: {
    arrinfo() {
      let arr = ["תנועת כננת לאורך הקורה", "הרמה והורדה של כבל כננת", ""];
      switch (this.craneKind) {
        case "עגורן גשר":
          arr[2] = "בעגורן גשר סטנדרטי ישנם 4 מנועים חשמליים:";
          break;
        case "עגורן שער":
          arr[2] = 'תנועת כל העגורן קדימה ואחורה ע"י גלגלי הסעה בתוך המסילות';
          break;
        case "עגורן עמוד":
          arr[2] = 'תנועת הקורה ימינה ושמאלה ע"י צידוד';
          break;
        default:
          arr = ["מידע לא זמין."];
      }
      return arr;
    },
  },
};
</script>

<style scoped>
#crane-operations {
  /* display: flex; */
  /* margin-top: 1rem; */
  /* background-color: white; */
  border-radius: 1rem;
  /* width: 55vw; */
  /* height: 25rem; */
  /* align-items: center;
    justify-content: space-between; */
}

.header {
  font-size: 1.8rem;
  text-align: center;
  font-weight: bold;
}

.bubble {
  background-color: white;
  border-radius: 1rem;
  padding: 1.5rem;
  width: 20rem;
}

.bubble-container {
    display: flex;
    height: 20rem;
    flex-direction: column;
    justify-content: space-evenly;
}
</style>
