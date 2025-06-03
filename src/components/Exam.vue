<template>
  <div id="exam">
    <p class="header">מבחן</p>
    <!-- <div class="middle-container"> -->

    <div class="container-quiz">
      <p class="tag-ques">שאלה מספר {{ this.numQues + 1 }}</p>

      <div class="question-container">
        <p class="question-title">{{ this.questions[this.numQues].title }}</p>
        <div
          class="container-answer"
          v-for="(answer, index) in this.questions[this.numQues].answers"
          :key="index"
        >
          <img
            :id="index"
            @click="theChosenAnswer(index)"
            class="question-squre"
            :src="getSrcAnswerSqure(index)"
          />
          <p class="ans-text">{{ answer }}</p>
        </div>
      </div>
    </div>
    <!-- </div> -->
    <div class="arrows-container">
      <img
        @click="prevQuestion"
        v-if="numQues > 0"
        class="moving-arrow back"
        src="/media/exam/left-arrow.svg"
      />
      <img
        v-if="numQues < 6"
        @click="nextQuestion"
        class="moving-arrow next"
        src="/media/exam/left-arrow.svg"
      />
    </div>

    <img src="/media/exam/disable-doneBtn.png" class="done-btn" />
    <div class="tracking-ans-container">
      <p class="bubble-ans" v-for="i in questions.length" :key="i">{{ i }}</p>
    </div>

    <p class="back-btn moving-btn" @click="prevPart">חזור</p>
  </div>
</template>

<script>
export default {
  name: "exam",
  props: [],
  data() {
    return {
      questions: [
        {
          Qtype: 0,
          title: "אילו מערכות נלוות לעגורנים העיליים?",
          answers: [
            "קדימה, אחורה, ימינה ושמאלה.",
            "הזנה, הסעה, הרמה והורדה.",
            "חשמל, פיקוד, הורדה והרמה.",
            "הסעה, פיקוד וחשמל.",
          ],
          correctAnswer: 3,
          numAnswer: 4,
          indexChosenAnswer: -1,
        },
        {
          Qtype: 1,
          title: "באיזה מצבים יתקינו בעגורנים תאים פוטואלקטריים כתוספת?",
          answers: [
            'בעגורנים שיועדו לביצוע החלפת חט"כ.',
            "במצבים בהם פועלים שני עגורנים באותו מסלול או כאשר יש לעגורן תחנות קבועות.",
            "במצבים בהם פועל עגורן עמוד באותו תא עבודה יחד עם עגורן שער.",
            'בעגורנים מסוג "עמוד" ו-"גשר".',
          ],
          correctAnswer: 1,
          numAnswer: 4,
          indexChosenAnswer: -1,
        },
        {
          Qtype: 2,
          title: "אילו תוספות מיוחדות יש למערכת החשמל בעגורנים?",
          answers: [
            "יחידות בקרה ממוחשבות המבצעות את הפעולות.",
            "מתגים, שקעים ותקעים.",
            "צופר, תאורה וחיישנים.",
            "לא קיימות תוספות מיוחדות.",
          ],
          correctAnswer: 2,
          numAnswer: 4,
          indexChosenAnswer: -1,
        },
        {
          Qtype: 3,
          title: "מהם חלקי הכננת החשמלית לכבל?",
          answers: [
            "מתנע, מנוע מכאני ושרשרת הנעה.",
            "מתנע, מנוע, רדיאטור ותוף כננת.",
            "מתנע, מנוע חשמלי, תוף כננת, ציר תנועה ומערכת הפחתה.",
            "מנוע הידראולי, גלגל שיניים ומצמד לחץ.",
          ],
          correctAnswer: 2,
          numAnswer: 4,
          indexChosenAnswer: -1,
        },
        {
          Qtype: 4,
          title: "חלקי הכננת המיועדים לשרשרת?",
          answers: [
            "גוף הכננת, שרשרת הרמה וקרס נעילה עצמית מאובטח.",
            "גוף, שרשרת הרמה, גלגל שיניים מיוחד, מיכל איסוף שרשרת וקרס.",
            "תוף הכננת, מנוע חשמלי ושרשרת.",
            "תוף הכננת, שרשרת נעילה עצמית וכבל בעל לב חבל.",
          ],
          correctAnswer: 1,
          numAnswer: 4,
          indexChosenAnswer: -1,
        },
        {
          Qtype: 5,
          title: "איזה סוגי כננות קיימים בעגורנים? ",
          answers: [
            " כננת חשמלית לכבל ולשרשרת, כננת מכאנית לכבל ולשרשרת.",
            "כננת חשמלית לכבל ושרשרת.",
            "כננת מכאנית לכבל ושרשרת.",
            "⁠כננת אוטומטית לכבל ושרשרת.",
          ],
          correctAnswer: 0,
          numAnswer: 4,
          indexChosenAnswer: -1,
        },
        {
          Qtype: 6,
          title: "איזה שיטות פיקוד קיימות בעגורנים?",
          answers: [
            ' ידית פיקוד ניידת לאורך הקורה, ידית פיקוד תלויה קבוע על הקורה, ידית פיקוד תלויה על הכננת, פיקוד מתוך תא, פיקוד ע"י שלט אלחוטי.',
            " ⁠פיקוד מתוך תא ",
            " ⁠פיקוד מתוך חלון, ידית פיקוד ניידת לאורך הקורה ",
            "ידית פיקוד תלויה קבוע על הקורה , ידית פיקוד תלויה על כננת חשמלית , פיקוד מתוך חדר. ",
          ],
          correctAnswer: 0,
          numAnswer: 4,
          indexChosenAnswer: -1,
        },
      ],
      numQues: 0,
    };
  },
  methods: {
    nextQuestion() {
      if (this.numQues !== 6) {
        this.numQues++;
      }
    },
    prevQuestion() {
      if (this.numQues !== 0) {
        this.numQues--;
      }
    },
    prevPart() {
      this.$emit("back-to-start-sign");
    },
    theChosenAnswer(index) {
      this.questions[this.numQues].indexChosenAnswer = index;
    },
    getSrcAnswerSqure(num) {
      // Determine the base URL (for local and production)
      const basePath =
        process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return num === this.questions[this.numQues].indexChosenAnswer
        ? `${basePath}media/exam/answer-squre-marked.svg`
        : `${basePath}media/exam/answer-squre-unmarked.svg`; // Static path to the images in the public folder
    },
  },
};
</script>

<style scoped>
#exam {
  width: 100vw;
  height: 100vh;
  display: flex;
  z-index: 1;
  flex-direction: column;
  align-items: center;
}

.ans-text {
  width: 30rem;
}

.container-quiz {
  width: 35rem;
  text-align: right;
  margin-top: 5rem;
}

.tracking-ans-container {
  background-color: #023047;
  width: 40rem;
  height: 5rem;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  border-radius: 3rem;
  position: absolute;
  bottom: 2rem;
}
/* .middle-container{
    display: flex;
} */

.moving-arrow {
  width: 4rem;
  position: absolute;
  top: 50%;
}

.back {
  transform: rotate(180deg) translateY(50%);
  right: 8rem;
}

.next {
  transform: translateY(-50%);
  left: 8rem;
}

.done-btn {
  position: absolute;
  width: 10rem;
  bottom: 2rem;
  left: 2rem;
}

.bubble-ans {
  background-color: #8cd0ec;
  color: #023047;
  /* color:white; */
  border-radius: 100%;
  width: 3rem;
  height: 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.question-container {
  margin-top: -3rem;
}

.container-answer {
  display: flex;
  /* margin-bottom: 0.1rem; */
}

.header {
  font-size: 2.5rem;
  font-weight: bolder;
  /* margin-top: 3rem; */
  position: absolute;
  right: 10rem;
}

.tag-ques {
  background-color: #023047;
  color: white;
  border-radius: 2rem;
  width: 10rem;
  height: 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.question-title {
  font-size: 2rem;
}

.question-squre {
  width: 2rem;
  margin-left: 1rem;
  cursor: pointer;
}

.moving-btn {
  z-index: 5;
  position: absolute;
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
  align-items: center; /* Vertically centers the text */
  text-align: center; /* Ensures the text is centered if multiline */
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.moving-btn:hover {
  background-color: #023047;
  color: white;
}

.back-btn {
  right: 1rem;
}

@media screen and (max-width: 600px) {
  #exam {
    width: 100vw;
    height: 91vh;
  }

  .tracking-ans-container {
    width: 22rem;
    bottom: 2rem;
    height: 8rem;
    flex-wrap: wrap;
  }

  .container-quiz {
    width: 30rem;
    margin-top: 8rem;
  }

  .moving-arrow {
    width: 4rem;
    position: static;
    /* bottom: 17rem; */
    top: auto;
  }

  .arrows-container {
    display: flex;
    width: 12rem;
    height: 10rem;
    flex-direction: row;
    align-items: center; 
    justify-content: space-evenly;
  }

  .done-btn {
    width: 10rem;
    bottom: 12rem;
  }

  .bubble-ans {
    margin-right: 1rem;
    margin-left: 1rem;
    margin-top: 0.1rem;
    margin-bottom: 0rem;
  }
}
</style>
