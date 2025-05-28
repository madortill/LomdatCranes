<template>
  <div id="final-highlights">
    <p class="header">דגשים אחרונים</p>
    <p class="sub-title">כללי ברזל אותם עליך לדעת לפני הפעלת מנוף:</p>
    <div class="for-computer">
      <div
        class="card-computer"
        v-for="i in sumNumCards"
        :key="i"
        :style="{ '--card-color': colorArr[i] }"
      >
        <p>{{ info[i] }}</p>
        <div v-if="i === 3">
          <p v-for="num in 3" :key="num">
            {{ info[num + sumNumCards + 1] }}
          </p>
        </div>
      </div>
    </div>
    <div class="for-phone">
      <p class="arrow" :class="counterCardPhone === 0 ? 'hide': ''"  @click="nextInfo(false)">{{arrArrows[1]}}</p>
      <div class="card-phone"  :style="{ '--card-color': colorArr[counterCardPhone] }">
        <p>{{ info[counterCardPhone] }}</p>
      </div>
      <p class="arrow" @click="nextInfo(true)" :class="counterCardPhone === 3 ? 'hide': ''">{{arrArrows[0]}}</p>
      
    </div>

    <p class="last-note-computer">{{ info[info.length - 1] }}</p>
  </div>
</template>

<script>
export default {
  name: "final-highlights",
  data() {
    return {
      arrArrows: [">", "<"],
      info: [
        "הגיל המינימלי לביצוע קורס מפעיל מנוף הוא 18.",
        "אסור לעבוד ללא תועלת מפעיל מנוף בתוקף.",
        "את התעודה יש לחדש כל שנתיים על ידי ביצוע מבחן במרכז מבחנים, כל שנה נדרש ריענון מקצועי על ידי נגד בעל רישיון עם שנה ותק לפחות.",
        'לאחר ביצוע ההכשרה אתם נדרשים לבצע חניכה ביחידה לפי הוראת קנטא"ר 0023.',
        "במסגרת החניכה עליכם לבצע 10 הפעלות לפחות עם חונך ולשלוח את המסמכים חתומים למרכז המבחנים תוך חודש ימים.",
        "שימו לב, במהלך החניכה אחוז המשקל בו אתם רשאים לעבוד הוא עד 40% מעומס העבודה הבטוח של המנוף.",
        "חייל שלא ישלח תיק חניכה (תוך 30 יום), הקורס יבטל ויאלץ לבצע קורס חוזר.",
      ],
      colorArr: ["#F88C01", "#FFAF02", "#8CD0EC", "#1E85AE"],
      counterCardPhone: 0,
      sumNumCards: [0, 1, 2, 3],
    };
  },

  methods: {
    nextInfo(up) {
      if( up && this.counterCardPhone < 3) {
        this.counterCardPhone++;
      } else if(!up && this.counterCardPhone > 0) {
        this.counterCardPhone--;
      }
    }
  },
};
</script>

<style scoped>
#final-highlights {
  height: 100vh;
  width: 100vw;
  color: black;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.hide {
  visibility: hidden;
}

.arrow {
  width: 4rem;
  height: 3rem;
  background-color: white;
  text-align: center;
  font-size: 2rem;
  border-radius: 50%;
  cursor: pointer;
  color: black;
  display: flex;
  align-items: center;
  justify-content: center;

}

.sub-title {
  margin-bottom: 3rem;
}

.header {
  font-weight: bold;
  font-size: 2.5rem;
}

.for-phone {
  width: 100%;
  height: 18rem;
  display: none;
}

.card-phone {
  background-color: var(--card-color);
  width: 11rem;
  height: 16rem;
  padding: 1rem;
  border-radius: 1rem;
  transition: all 0.2s;

}

.for-computer {
  display: flex;
  width: 100vw;
  justify-content: space-evenly;
}
.card-computer {
  background-color: var(--card-color);
  width: 11rem;
  height: 16rem;
  padding: 1rem;
  border-radius: 1rem;
  display: flex;
  align-items: center;
}

.last-note-computer {
  font-weight: bold;
  font-size: 1.5rem;

}

@media screen and (max-width: 600px) {
  #final-highlights {
    height: 91vh;
  }

  .for-computer {
    display: none;
  }

  .last-note-computer {
    font-weight: none;
  }

  .for-phone {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
  }
}
</style>
