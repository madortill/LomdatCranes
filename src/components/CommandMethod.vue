<template>
  <div id="command-method">
    <div class="pop-out">
        <p class="moving-btn" @click="finishedTheMethod">אוקיי</p>
    </div>
    <div class="cloud">
        <p class="cloud-text">{{ cloudObject.text }}</p>
        <img class="cloud-img" :src="cloudObject.src" alt="cloud img"/>
    </div>
  </div>
</template>

<script>
export default {
  name: "command-method",
  props: ['cloudObject'],
  data() {
    return {
      theInfo: [
        [
          "אז מה זה עגורן עילי?",
          "עגורנים עיליים הם סוגי מנופים נייחים שלא מובנים על רכב, אלא מותקנים בסדנא ונותנים שירות בדרך כלל בפסי ייצור וכדומה.",
          "קיימות 4 דרגות רישיון הפעלה בעגורנים: א-ב, ג-ד.",
        ],
        [
          "כללי בטיחות",
          "ישנם מספר כללי בטיחות אותם יש לבדוק לפני שניגש לביצוע עבודה עם המנוף:",
        ],
        ["תוספות פוטנציאליות בעגורנים"],
        ["מערכת החשמל בעגורנים", "אחראית על 3 מערכות עיקריות:"],
      ],
      titlesInElectricalSystemArr: ["הסעה", "פיקוד", "חשמל"],
    };
  },
  methods: {
    finishedTheMethod() {
        this.$emit('finished-method', false);
    }
  },
  computed: {},
};
</script>

<style scoped>
#command-method {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.pop-out {
  background-color: #023047;
  /* padding: 1rem; */
  border-radius: 1rem;
  position: absolute;
  /* color: white; */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -35%);
  height: 27rem;
  width: 55%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.moving-btn {
  z-index: 1;
  position: absolute;
  bottom: 1rem;
  left: 50%;
  transform: translateX(-50%);
  width: 5rem;
  height: 3rem;
  font-size: 1rem;
  background-color: var(--moving-btn-color);
  border-radius: 1.5rem;
  padding: 0; /* Remove padding to ensure centering works properly */
  /* Centering the text */
  display: flex;
  justify-content: center; /* Horizontally centers the text */
  align-items: center; /* Vertically centers the text */
  text-align: center; /* Ensures the text is centered if multiline */
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.moving-btn:hover {
  background-color: #023047;
  color: white;
}

.cloud {
    position: absolute;
    top: 9rem;
    right: 9rem;
width: 22rem;
}

.cloud-text {
    position: relative;
    z-index: 3;
    top: 7rem;
}

.cloud-img {
    position: relative;
z-index: 2;
}

@media screen and (max-width: 700px) {
    .pop-out {
  /* transform: translate(-50%, -40%); */
  height: 40rem;
  width: 90%;

}

.cloud {
    /* width: 22rem; */
    /* position: absolute; */
    top: 10rem;
    right: auto;
    /* left: 50%;
    transform: translateX(-50%); */
}
}
</style>
