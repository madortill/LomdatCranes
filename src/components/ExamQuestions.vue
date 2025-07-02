<template>
  <div id="exam-questions">
    <p class="header">מבחן</p>
    <div class="container-quiz">
      <p class="tag-ques">שאלה מספר {{ this.numQues + 1 }}</p>

      <div class="question-container">
        <p class="question-title">{{ this.shuffledQuestions[this.numQues].title }}</p>
        <div
          class="container-answer"
          v-for="(answer, index) in this.shuffledQuestions[this.numQues].answers"
          :class="[
            this.shuffledQuestions[this.numQues].correctAnswer === index && checkAns
              ? 'correct-answer'
              : '',
            this.shuffledQuestions[this.numQues].indexChosenAnswer !==
              this.shuffledQuestions[this.numQues].correctAnswer &&
            this.shuffledQuestions[this.numQues].indexChosenAnswer === index &&
            checkAns
              ? 'false-answer'
              : '',
          ]"
          :key="index"
        >
          <img
            :id="index"
            @click="theChosenAnswer(index)"
            class="question-squre"
            :class="checkAns ? 'disable' : 'able'"
            :src="getSrcAnswerSqure(index)"
          />
          <p class="ans-text">{{ answer }}</p>
        </div>
      </div>
    </div>
    <div class="arrows-container">
      <img
        @click="prevQuestion"
        v-if="this.numQues > 0"
        class="moving-arrow back"
        src="/media/exam/left-arrow.svg"
      />
      <img
        v-if="this.numQues < 6"
        @click="nextQuestion"
        class="moving-arrow next"
        src="/media/exam/left-arrow.svg"
      />
    </div>

    <img
      :src="getSrcDoneBtn()"
      class="done-btn"
      :class="canBeSub ? 'done-active-btn' : ''"
      @click="toSubmit"
    />
    <div class="tracking-ans-container">
      <p
        class="bubble-ans"
        v-for="i in shuffledQuestions.length"
        :key="i"
        :id="i"
        @click="showQuestion"
        :class="[
          this.numQues + 1 === i ? 'present-bubble' : '',
          shuffledQuestions[i - 1].indexChosenAnswer === -1
            ? 'unmarked-bubble'
            : 'marked-bubble',
        ]"
      >
        {{ i }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "exam-questions",
  props: ["checkAns", "numQues"],
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
      canBeSub: false,
      shuffledQuestions: [],
    };
  },
  created() {
    this.shuffleQuestions();
  },
  watch: {
    checkAns(newVal) {
      if (!newVal) {
        this.resetChosenAnswers();
      }
    },
  },
  methods: {
    shuffleQuestions() {
      const shuffled = this.questions.slice(); // שומר על המקור
      for (let i = shuffled.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
      }
      this.shuffledQuestions = shuffled;
    },
    //מופעל כשהמשתמש נכשל במבחן וזהו בעצם איפוס התשובות
    resetChosenAnswers() {
      this.shuffledQuestions.forEach((question) => {
        question.indexChosenAnswer = -1;
      });
      this.canBeSub = false;
    },
    toSubmit() {
      if (this.canBeSub) {
        let score = 0;
        let NumQuestions = this.shuffledQuestions.length;
        //חישוב כמה כל תשובה נכונה שווב בניקוד
        let correctPoints = 100 / Number(NumQuestions);
        //סופר כמה תשובות נכונות מתוך כל השאלות
        let counterCorrect = 0;
        let ques = null;
        for (let i = 0; i < NumQuestions; i++) {
          ques = this.shuffledQuestions[i];
          if (ques.correctAnswer === ques.indexChosenAnswer) {
            score += correctPoints;
            counterCorrect++;
          }
        }
        this.$emit("show-results", score, counterCorrect, NumQuestions);
      }
    },
    showQuestion(event) {
      this.$emit("change-current-num-ques", event.currentTarget.id - 1);
    },

    checkIfCanBeSub() {
      for (let i = 0; i < this.shuffledQuestions.length; i++) {
        if (this.shuffledQuestions[i].indexChosenAnswer === -1) {
          return false;
        }
      }
      return true;
    },

    nextQuestion() {
      if (this.numQues !== 6) {
        this.$emit("change-current-num-ques", true);
      }
    },
    prevQuestion() {
      if (this.numQues !== 0) {
        this.$emit("change-current-num-ques", false);
      }
    },
    theChosenAnswer(index) {
      this.shuffledQuestions[this.numQues].indexChosenAnswer = index;
      if (this.checkIfCanBeSub()) {
        this.canBeSub = true;
      }
    },
    getSrcAnswerSqure(num) {
      // Determine the base URL (for local and production)
      const basePath =
        process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return num === this.shuffledQuestions[this.numQues].indexChosenAnswer
        ? `${basePath}media/exam/answer-squre-marked.svg`
        : `${basePath}media/exam/answer-squre-unmarked.svg`;
    },
    getSrcDoneBtn() {
      const basePath =
        process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return !this.canBeSub
        ? `${basePath}media/exam/disable-doneBtn.png`
        : `${basePath}media/exam/doneBtn.png`;
    },
  },
};
</script>

<style scoped>
#exam-questions {
  width: 100vw;
  height: 100vh;
  display: flex;
  z-index: 1;
  flex-direction: column;
  align-items: center;
}

.correct-answer {
  background-color: rgb(128, 202, 128);
  border-radius: 1rem;
  padding: 0.1rem;
}

.false-answer {
  background-color: rgb(241, 114, 114);
  border-radius: 1rem;
  padding: 0.1rem;
}

.done-active-btn {
  cursor: pointer;
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

.moving-arrow {
  width: 4rem;
  position: absolute;
  top: 50%;
  cursor: pointer;
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

.unmarked-bubble {
  background-color: #7ba4b6;
}

.marked-bubble {
  background-color: #8cd0ec;
}

.present-bubble {
  background-color: #ffffff;
}

.bubble-ans {
  color: #023047;
  border-radius: 100%;
  width: 3rem;
  height: 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.question-container {
  margin-top: -3rem;
}

.container-answer {
  display: flex;
}

.header {
  font-size: 2.5rem;
  font-weight: bolder;
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
}

.able {
  pointer-events: all;
  cursor: pointer;
}

.disable {
  pointer-events: none;
  cursor: none;
}

@media screen and (max-width: 600px) {
  .container-answer {
    align-items: center;
  }

  #exam-questions {
    width: 100vw;
    height: 91vh;
  }

  .question-container {
    height: 30rem;
  }

  .tracking-ans-container {
    width: 29rem;
    height: 5rem;
  }

  .container-quiz {
    width: 30rem;
    margin-top: 7rem;
  }

  .moving-arrow {
    width: 4rem;
    position: static;
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
    width: 7rem;
    bottom: auto;
    left: 1rem;
    top: 4rem;
  }

  .header {
    right: 1rem;
  }
}
</style>
