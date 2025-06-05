<template>
  <div id="crane-components">
    <p class="header fix-header" :class="showZoom ? 'fade-out-animation' : ''">
      מרכיבים בעגורן
    </p>
    <object
      :class="[
        showZoom ? 'with-zoom' : 'without-zoom',
        numPart === 1 ? 'to-orange-zoom' : '',
        numPart === 2 ? 'to-blue-zoom' : '',
      ]"
      class="img-crane"
      type="image/svg+xml"
      :data="craneUrl"
    ></object>

    <div
      class="info-container"
      v-if="numPart < 3"
      :class="{
        'fade-in-animation': showInfo,
        'fade-out-animation': showFadeOutInfo,
        'info-in-yellow': numPart === 0,
        'info-in-orange': numPart === 1,
        'info-in-blue': numPart === 2,
      }"
      :style="{ '--bg-color': arrBgColors[numPart] }"
    >
      <p class="header">{{ arrInfo[numPart][0] }}</p>
      <p
        class="text"
        v-for="(item, index) in arrInfo[numPart].slice(1)"
        :key="index"
      >
        {{ item }}
      </p>
      <p class="moving-btn" @click="nextPart">הבנתי!</p>
    </div>
    <p v-if="finishLearning" class="again" @click="startOver">שוב !</p>
  </div>
</template>

<script>
export default {
  name: "crane-components",
  props: ["finishLearning"],
  data() {
    return {
      showZoom: false,
      numPart: 0,
      arrBgColors: ["#E6BC4D", "#F78C1E", "#2085AE"],
      arrInfo: [
        [
          "מפסקי גבול",
          "לכל כננת חשמלית בעגורן יש מפסק גבול, המפסיק את פעולות המנוע בדיוק לפני סוף המהלך.",
          "תפקידו של המפסק למנוע נזק לעגורן או לציוד הסובב אותו.",
          "ישנו מפסק גבול נוסף שתפקידו להאט את מהירות הכננת כאשר הוא קרוב לסופה של קורה.",
        ],
        [
          "מפסקי זרם",
          "מפסק זרם הוא רכיב אשר מאפשר ניתוק של חשמל.",
          "בכל סדנא נמצא מפסק זרם ראשי  שתפקידו להפסיק את הזרם החשמלי בעת סכנה או פגיעה.",
          " מפסק זרם לעגורן: בעגורן נמצא מפסק זרם להדלקה וכיבוי המנוף. בכל סיום פעולה יש לנתק את המנוף על ידי המפסק.",
          "פטריית חירום: ממוקמת על השלט, מיועדת להפסקת הזרם במקרה חירום בעזרת לחיצה. בסיבוב הפטרייה לצד ימין יפתח הזרם החשמלי לתחילת או המשך עבוד",
        ],
        [
          "תאים פוטואלקטריים",
          "  חיישני אור (לייזרים), אשר תפקידם הוא זיהוי ובקרה. התאים בנויים בצורה שבתוכם יש חומר שמוליך זרם חשמלי רק כאשר פוגע בו אור. בעגורנים העיליים מותקנים תאים פוטואלקטריים כאשר: קיימים שני עגורנים על אותו מסלול, לעגורן יש תחנות קבועות (לדוגמה: בפסי יצור של מפעלים שונים).",
        ],
      ],
      showInfo: false,
      showFadeOutInfo: false,
    };
  },
  methods: {
    nextPart() {
      //שלא יהיה אפשר ללחוץ מלא פעמים
      if (this.showInfo) {
        this.showInfo = false;
        this.showFadeOutInfo = true;
        if (this.numPart === 2) {
          this.numPart++;
          this.showZoom = false;
          setTimeout(() => {
            this.$emit("show-next-btn");
            this.$emit("update-finish-learning", true);
          }, 1000);
        } else {
          setTimeout(() => {
            this.numPart++;
          }, 200);
          setTimeout(() => {
            this.showInfo = true;
            this.showFadeOutInfo = false;
          }, 1200);
        }
      }
    },
    startOver() {
      this.numPart = 0;
      this.showFadeOutInfo = false;
      this.$emit("update-finish-learning", false);
      this.showZoom = true;
      setTimeout(() => {
        this.showInfo = true;
      }, 3000);
    },
  },
  mounted() {
    if (!this.finishLearning) {
      setTimeout(() => {
        this.showZoom = true;
        setTimeout(() => {
          this.showInfo = true;
        }, 3000);
      }, 1000); // The zoom effect is triggered after 700ms
    }
  },
  computed: {
    craneUrl() {
      const baseUrl = import.meta.env.BASE_URL; // Get the correct base URL
      return `${baseUrl}media/theCraneInCraneComponents.svg`;
    },
  },
};
</script>

<style scoped>
#crane-components {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  position: relative;
  z-index: -1;
}

.again {
  background-color: white;
  color: #023047;
  font-size: 2rem;
  position: absolute;
  top: 10rem;
  padding: 1rem;
  left: 30rem;
  transform: rotate(-20deg);
  border-radius: 1rem;
  cursor: pointer;
  transition: all 0.2s;
}

.again:hover {
  color: white;
  background-color: #023047;
}

.img-crane {
  margin-bottom: -1rem;
  position: relative; /* Add position to make z-index work */
  transition: transform 3s ease-in, width 3s ease-in, margin-top 3s ease-in,
    margin-left 3s ease-in;
  z-index: -1; /* Ensure z-index is applied */
}

.without-zoom {
  width: 30rem; /* Set the initial size */
  margin-bottom: -1rem;
  margin-top: 0rem;
  transition: transform 1s ease-in, width 1s ease-in, margin-top 1s ease-in,
    margin-left 1s ease-in;
}

.with-zoom {
  width: 280rem; /* Adjust width for zoom effect */
  margin-top: -176rem;
  margin-left: 190rem;
}

.to-orange-zoom {
  margin-top: -146rem;
  margin-left: 177.7rem;
  transition: transform 1s ease-in, width 1s ease-in, margin-top 1s ease-in,
    margin-left 1s ease-in;
}

.to-blue-zoom {
  margin-top: -156rem;
  margin-left: 114.9rem;
  transition: transform 1s ease-in, width 1s ease-in, margin-top 1s ease-in,
    margin-left 1s ease-in;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 1.3rem;
}

.fix-header {
  margin-top: 8rem;
}

.fade-out-animation {
  animation: fadeOut 0.2s linear forwards;
}

@keyframes fadeOut {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    visibility: hidden;
  }
}

.info-container {
  position: absolute;
  background-color: var(--bg-color);
  left: 50%;
  opacity: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.info-in-yellow {
  width: 41rem;
  transform: translateX(-43.7%);
  height: 23.2rem;
  top: 13.2rem;
}

.info-in-orange {
  width: 35.2rem;
  transform: translateX(-50%);
  height: 28.8rem;
  top: 12.4rem;
}

.info-in-blue {
  width: 23.5rem;
  transform: translateX(-50%);
  height: 35rem;
  top: 9rem;
}

.fade-in-animation {
  animation: fadeIn 0.2s linear forwards;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.moving-btn {
  z-index: 1;
  position: absolute;
  bottom: 0rem;
  left: 50%;
  transform: translateX(-50%);
  width: 5rem;
  height: 3rem;
  font-size: 1rem;
  background-color: var(--moving-btn-color);
  border-radius: 1.5rem;
  padding: 0; 
  /* Centering the text */
  display: flex;
  justify-content: center; 
  align-items: center; 
  text-align: center; 
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.moving-btn:hover {
  background-color: #023047;
  color: white;
}

.text {
  margin: 0rem;
  width: 95%;
}

@media screen and (max-width: 600px) {
  #crane-components {
    height: 91vh;
  }

  .with-zoom {
    width: 260rem; /* Adjust width for zoom effect */
    margin-top: -156rem;
    margin-left: 179rem;
  }

  .to-orange-zoom {
    margin-top: -130rem;
    margin-left: 165rem;
  }

  .to-blue-zoom {
    margin-top: -140rem;
    margin-left: 106.5rem;
  }

  .info-in-yellow {
    width: 30rem;
    height: 21.5rem;
    top: 20.3rem;
    transform: translateX(-49.5%);
  }

  .info-in-orange {
    width: 32.5rem;
    transform: translateX(-50%);
    height: 26.4rem;
    top: 17.6rem;
  }

  .info-in-blue {
    width: 21.7rem;
    height: 35rem;
    top: 13.8rem;
  }

  .again {
    top: 15rem;
    left: 20%;
    transform: rotate(-20deg), translateX(-50%);
  }
}

@supports (-webkit-touch-callout: none) {
  /* זיהוי של מכשירי iOS */

  @media screen and (max-width: 600px) {
    .with-zoom {
      width: 260rem;
      margin-top: -150rem;
      /* margin-left: 161rem; */
    }
    #crane-components {
      overflow: visible; /* מאפשר להרחיב את התמונה מחוץ למסך */
    }
  }
}
</style>
