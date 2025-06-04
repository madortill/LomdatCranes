<template>
  <div id="start-sign">
    <img class="start-sign-img" src="/media/StartSign.png" alt="startSign" />
    <div class="text-container" v-if="thePart === 0">
      <p>בחרת ב -</p>
      <p class="partOfLomda">{{ arrPartTitle[sectionNum] }}</p>
      <p>אם תרצה לשנות את בחירתך אפשר ללחוץ על כפתור הבית</p>
      <p class="goodWord">בהצלחה!</p>
    </div>
    <!-- <div class="text-container" v-if="!firstChosen && thePart === 0">
      <p>כל הכבוד סיימת את החלק ה{{ arrFinishedPart[sectionNum - 1] }}</p>
      <p>עכשיו נעבור לחלק ה{{ arrFinishedPart[sectionNum] }} של הלומדה</p>
      <p class="partOfLomda">{{ arrPartTitle[sectionNum] }}</p>
      <p class="goodWord">בהצלחה!</p>
    </div> -->
    <div
      class="text-container fixPosition"
      v-if="sectionNum === 0 && thePart === 1"
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

    <div class="text-container" v-if="sectionNum === 1 && thePart === 1">
      <p>עכשיו נלמד כיצד להפעיל עגורן גשר על ידי המחשות ויזואליות</p>
      <p class="partOfLomda">לשים לב</p>
      <p>בצד העליון של המסך תופיע ההוראה לפעולה שתצטרכ/י לממש</p>
    </div>

    <!-- לגבי המבחן -->
    <div class="text-container" v-if="sectionNum === 2 && thePart === 1">
      <p>
        אתם תעברו עכשיו מבחן על החומר שלמדתם בלומדה, המבחן עם ציון אז וודאו שאתם
        מרגישים מוכנים
      </p>
      <p>המבחן מכיל 7 שאלות אמריקאיות</p>
      <p>שימו לב שלאחר לחיצה על הבא אין דרך לחזור</p>

      <p class="text-next-to-input">הכניסו את שמכם המלא:</p>
      <input
        class="input-tag"
        placeholder="הקלידו כאן שם מלא"
        v-model="fullName"
        lang="he"
        type="text"
      />
      <br />
      <p class="text-next-to-input">הכניסו מספר אישי:</p>
      <input
        class="input-tag"
        placeholder="הקלידו כאן מספר אישי"
        v-model="idNumber"
        lang="he"
        type="text"
        maxlength="7"
      />
    </div>

    <p
      class="next-btn moving-btn"
      @click="nextPart"
      :class="{ disable: !isFormValid() }"
    >
      הבא
    </p>
    <p
      v-if="thePart !== 0 || isAContinuance"
      class="back-btn moving-btn"
      @click="prevPart"
    >
      חזור
    </p>
  </div>
</template>

<script>
export default {
  name: "start-sign",
  props: ["sectionNum", "firstChosen", "thePart", "isAContinuance"],
  data() {
    return {
      arrPartTitle: ["תחילת הלומדה", "תפעול", "מבחן"],
      // arrFinishedPart: ["ראשון", "שני", "שלישי"],
      array1: [
        "מטרת על",
        "הלומד יסביר את אופן התפעול של עגורן עילי.",
        "מטרות ביניים",
        "הלומד יפרט את סוגי העגורנים העיליים.",
        "הלומד יפרט את מערכות העגורן.",
        "הלומד יזהה את חלקיו השונים של העגורן.",
      ],
      //קשור למבחן
      fullName: "",
      idNumber: "",
    };
  },
  methods: {
    nextPart() {
      if (this.sectionNum === 2 && this.thePart === 1) {
        this.$emit("send-exam-variables", this.fullName, this.idNumber);
      }
      this.$emit("to-next-board");
    },

    prevPart() {
      if (this.isAContinuance && this.thePart === 0) {
        this.$emit("back-to-general-material");
      } else {
        this.$emit("to-prev-board");
      }
    },
    toShowCloudBg(show) {
      this.$emit("to-show-cloud-bg", show);
    },

    submitForm() {
      // כאן תוכל לשמור או לשלוח את הנתונים
      alert(`שם מלא: ${this.fullName}\nמספר אישי: ${this.idNumber}`);
    },
    isFormValid() {
      if (this.sectionNum === 2 && this.thePart === 1) {
        // שם מלא - לפחות 2 מילים (מופרדות ברווח)
        const words = this.fullName.trim().split(/\s+/);
        const fullNameValid =
          words.length >= 2 && words.every((word) => word.length > 0);

        // מספר אישי - 7 ספרות בלבד
        const idNumberValid = /^\d{7}$/.test(this.idNumber);

        return fullNameValid && idNumberValid;
      } else {
        return true;
      }
    },
  },
};
</script>

<style scoped>
#start-sign {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  color: white;
  align-items: flex-end;
}

.text-next-to-input {
  display: inline;
}

.input-tag {
  border: none;
  border-radius: 1rem;
  width: 20rem;
  height: 3rem;
  margin-bottom: 1rem;
  background-color: #ffffff;
  font-weight: 500;
  font-size: 1em;
  text-align: center;
  color: black;
}

.talk-text {
  margin: 1rem;
  animation: floatAnimation 3s ease-in-out infinite;
  color: #8cd0ec;
  font-size: 3rem;
  border-radius: 10px;
  position: relative;
  cursor: default;
  width: fit-content;
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
  width: fit-content;
}

.info-text-goal:hover {
  background-color: #8cd0ec;
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
}

.header {
  font-weight: bold;
  font-size: 2.5rem;
}

.fixPosition {
  width: 45vw;
  height: 74%;
}

.moving-btn {
  /* z-index: 1; */
  position: absolute;
  bottom: 1rem;
  width: 5rem;
  height: 3rem;
  font-size: 1rem;
  background-color: #8cd0ec;
  border-radius: 1.5rem;
  padding: 0;
  /* Centering the text */
  display: flex;
  justify-content: center; /* Horizontally centers the text */
  align-items: center;
  text-align: center;
  transition: background-color 0.3s ease;
}

.moving-btn:hover {
  background-color: #023047;
  color: white;
}

.next-btn {
  left: 1rem;
}

.back-btn {
  right: 1rem;
}

.disable {
  background: rgb(182, 182, 182);
  cursor: auto;
  pointer-events: none;
}

.disable:hover {
  background: rgb(182, 182, 182);
  cursor: auto;
}

@media screen and (max-width: 600px) {
  .fixPosition {
    width: 74vw;
    height: 64%;
  }

  .start-sign-img {
    margin-bottom: -1rem;
  }

  .text-next-to-input {
    display: block;
  }
}
</style>
