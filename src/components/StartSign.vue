<template>
  <div id="start-sign">
    <img
      class="start-sign-img"
      src="/media/StartSign.png"
      alt="startSign"
    />
    <div class="text-container" v-if="firstChosen && thePart === 0">
      <p>בחרת ב -</p>
      <p class="partOfLomda">{{ arrPartTitle[partNum] }}</p>
      <p>אם תרצה לשנות את בחירתך אפשר ללחוץ על כפתור הבית</p>
      <p class="goodWord">בהצלחה!</p>
    </div>
    <div class="text-container" v-if="!firstChosen">
      <p>כל הכבוד סיימת את החלק ה{{ arrFinishedPart[partNum - 1] }}</p>
      <p>עכשיו נעבור לחלק ה{{ arrFinishedPart[partNum] }} של הלומדה</p>
      <p class="partOfLomda">{{ arrPartTitle[partNum] }}</p>
      <p class="goodWord">בהצלחה!</p>
    </div>
    <div
      class="text-container fixPosition"
      v-if="partNum === 0 && thePart === 1"
    >
      <p class="header">מטרות השיעור</p>
      <p
        v-for="(text, index) in array1"
        :key="text"
        :class="{
          'talk-text': index === 0 || index === 2,
          'info-text-goal': index !== 0 && index !== 2,
        }"
        :style="{
          'font-size': index === 0 || index === 2 ? '1.7rem' : '1rem',
        }"
      >
        {{ text }}
      </p>
    </div>
    <div v-if="partNum > 0 && firstChosen && showWarning">
      <div class="shadow"></div>
      <div class="warning-container">
        <p>שימו לב!</p>
        <p>אם לא תתחיל מתחילת הלומדה אז ציונך לא יעלה למפקדיך</p>
      </div>
    </div>

    <p @click="nextBoard" class="next-btn">הבא</p>
  </div>
</template>

<script>
export default {
  name: "start-sign",
  props: ["partNum", "firstChosen"],
  data() {
    return {
      arrPartTitle: ["תחילת הלומדה", "תפעול", "תרגול"],
      arrFinishedPart: ["ראשון", "שני", "שלישי"],
      thePart: 0,
      showWarning: true,
      array1: [
        "מטרת על",
        'הלומד יסביר את אופן התפעול של עגורן עילי.',
        "מטרות ביניים",
        'הלומד יפרט את סוגי העגורנים העיליים.',
        'הלומד יפרט את מערכות העגורן.',
        'הלומד יזהה את חלקיו השונים של העגורן.',
      ],
    };
  },
  mounted() {
    // Set a timeout to hide the warning after 3 seconds
    let timer = setTimeout(() => {
      this.showWarning = false;
      clearTimeout(timer);
    }, 2500);
  },
  methods: {
    nextBoard() {
      if (this.partNum === 0 && this.thePart === 0) {
        this.thePart++;
      } else {
        this.$emit('toNextBoard');
      }
    },
  },
};
</script>

<style scoped>
.talk-text {
  margin: 1rem;
  animation: floatAnimation 3s ease-in-out infinite;
  color: #8cd0ec;
  font-size: 3rem;
  border-radius: 10px;
  /* top: 1.5%; */
  /* text-decoration: none; */
  position: relative;
  cursor: default;
  width: fit-content;
  /* text-align: center; */
}

.talk-text:hover::before {
  visibility: visible;
  transform: scaleX(1);
}

.talk-text::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  bottom: 0;
  background-color: #8cd0ec;
  visibility: hidden;
  transform: scaleX(0);
  transition: all 0.3s ease-in-out 0s;
}

.info-text-goal {
  background-color: none;
  border-radius: 30px;
  height: 6%;
  transition: background-color 0.3s ease;
  margin: 2%;
  padding: 0.5%;
  /* text-align: center; */
  width: fit-content;
}

.info-text-goal:hover {
  background-color: #8cd0ec;
}

#start-sign {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  color: white;
  align-items: flex-end;
}
.goodWord {
  color: #8cd0ec;
  font-size: 1.5rem;
}

.partOfLomda {
  color: #ffb703;
  font-size: 2.5rem;
  margin: 0rem;
}

.start-sign-img {
  width: 60rem;
  height: 95%;
  z-index: 0;
  margin-bottom: -3rem;
  margin-right: 1rem;
  margin-left: 1rem;
}

.text-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* display: flex
;
    flex-direction: column;
    align-items: center; */
}

.shadow {
  top: 0rem;
  left: 0rem;
  position: absolute;
  background-color: black;
  opacity: 0.5;
  width: 100vw;
  height: 100vh;
}

.warning-container {
  background-color: white;
  color: red;
  width: 30rem;
  height: 10rem;
  z-index: 5;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.next-btn {
  position: absolute;
  left: 1rem;
  bottom: 1rem;
  width: 5rem;
  height: 3rem;
  font-size: 1rem;
  background-color: #8cd0ec;
  border-radius: 1.5rem;
  padding: 0; /* Remove padding to ensure centering works properly */
  /* Centering the text */
  display: flex;
  justify-content: center; /* Horizontally centers the text */
  align-items: center;     /* Vertically centers the text */
  text-align: center;      /* Ensures the text is centered if multiline */
  transition: background-color 0.3s ease;
}

.next-btn:hover {
  background-color: #023047;
  color: white;
}

.header {
  font-weight: bold;
  font-size: 2.5rem;
}

.fixPosition {
  width: 50vw;
  height: 60%;
}
</style>
