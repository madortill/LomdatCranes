<template>
  <div id="command-method">
    <div class="pop-out"></div>
    <div class="cloud"></div>
    <p class="moving-btn" @click="finishedTheMethod">אוקיי</p>
  </div>
</template>

<script>
export default {
  name: "command-method",
  props: [],
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
  transform: translate(-50%, -50%);
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

@media screen and (max-width: 700px) {
}
</style>
