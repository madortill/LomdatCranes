<template>
  <div id="final-highlights">
    <p class="header">דגשים אחרונים</p>
    <p class="sub-title">כללי ברזל אותם עליך לדעת לפני הפעלת מנוף</p>
    <div class="for-computer">
      <div class="card-computer" v-for="i in sumNumCards" :key="i">
        <p >{{ info[i] }}</p>
        <div v-if="i === 3">
          <p  v-for="num in 3" :key="num">{{ info[num + sumNumCards + 1] }}</p>
        </div>
      </div>
    </div>
    <div class="for-phone">
      <p>{{ info[counterCardPhone] }}</p>
    </div>
    <p class="last-note-computer">{{ info[info.length-1] }}</p>

  </div>
</template>

<script>
export default {
  name: "final-highlights",
  data() {
    return {
      info: [
        "הגיל המינימלי לביצוע קורס מפעיל מנוף הוא 18.",
        "אסור לעבוד ללא תועלת מפעיל מנוף בתוקף.",
        "את התעודה יש לחדש כל שנתיים על ידי ביצוע מבחן במרכז מבחנים, כל שנה נדרש ריענון מקצועי על ידי נגד בעל רישיון עם שנה ותק לפחות.",
        'לאחר ביצוע ההכשרה אתם נדרשים לבצע חניכה ביחידה לפי הוראת קנטא"ר 0023.',
        "במסגרת החניכה עליכם לבצע 10 הפעלות לפחות עם חונך ולשלוח את המסמכים חתומים למרכז המבחנים תוך חודש ימים.",
        "שימו לב, במהלך החניכה אחוז המשקל בו אתם רשאים לעבוד הוא עד 40% מעומס העבודה הבטוח של המנוף.",
        "חייל שלא ישלח תיק חניכה, הקורס יבטל ויאלץ לבצע קורס חוזר.",
      ],
      counterCardPhone: 0,
      sumNumCards: [0,1,2,3],
    };
  },

  methods: {},
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

.header {
  font-weight: bold;
  font-size: 2.5rem;
}

.for-phone {
  display: none;
  background-color: white;
    width: 10rem;
    height: 20rem;
}

.for-computer {
    display: flex;
    width: 100vw;
    justify-content: space-evenly;
  }
.card-computer {
  background-color: white;
    width: 11rem;
    height: 16rem;
    padding: 1rem;
    border-radius: 1rem;
}
   
.last-note-computer {
  font-weight: bold;
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
    display: block;
  }
}
</style>
