<template>
  <div id="american-questions" @click="checkAnswer">
      <h1 class="title-questionMultiple">
        {{ this.questions[this.numQues].title }}
      </h1>
      <h2
        class="second-instraction"
        v-if="this.questions[this.numQues].Qtype === 1"
      >
        בחר/י בשלוש התשובות הנכונות.
      </h2>
      <div class="div-mulQ">
        <div class="row">
          <button id="1" ref="1" class="pulse-button-hover">
            {{ this.questions[this.numQues].ans1 }}
          </button>
          <button id="2" ref="2" class="pulse-button-hover">
            {{ this.questions[this.numQues].ans2 }}
          </button>
          <button v-if="this.questions[this.numQues].Qtype === 1" id="5" ref="5" class="pulse-button-hover">
            {{ this.questions[this.numQues].ans5 }}
          </button>
        </div>
        <div class="row">
          <button id="3" ref="3" class="pulse-button-hover">
            {{ this.questions[this.numQues].ans3 }}
          </button>
          <button id="4" ref="4" class="pulse-button-hover">
            {{ this.questions[this.numQues].ans4 }}
          </button>
          <button v-if="this.questions[this.numQues].Qtype === 1" id="6" ref="6" class="pulse-button-hover">
            {{ this.questions[this.numQues].ans6 }}
          </button>
        </div>
      </div>
      <h1 class="finish" v-if="showFinish">כל הכבוד !</h1>

      <button class="moving-btn back-btn" @click="backToInfo">חזור</button>
  </div>
</template>

<script>
export default {
  name: "american-questions",
  // props: ['questions'],
  data() {
    return {
      numQues: 0,
      showFinish: false,
      showNextBtn: false,
      clickeAnswer: false,
      arrayChosenCorrect: ["", "", ""],
      questions: [
        {
          Qtype: 0,
          title: "לאיזה סוג עגורנים נוסמך?",
          ans1: "עגרונים מסוג א-ב",
          ans2: "עגורנים מסוג ד-ה",
          ans3: "עגורנים מסוג ג-ד",
          ans4: "אנחנו נוסמך על כל העגרונים הקיימים",
          correctAnswer: 3,
          numAnswer: 4,
        },
        {
          Qtype: 1,
          title: "איזה סוגי עגורנים קיימים?",
          ans1: "עגורן יד",
          ans2: "עגורן עמוד",
          ans3: "עגורן שער",
          ans4: "עגורן גשר",
          ans5: "עגורן כבל",
          ans6: "עגורן ידית",
          correctAnswer: [2, 3, 4],
          numAnswer: 6,
        },
        {
          Qtype: 2,
          title: "האם ניתן לסובב את הקורה בעגורן גשר?",
          ans1: "לא. עגורן גשר זז כגשר מעל המטען",
          ans2: "כן. ניתן לסובב את הקורה בעגורן",
          ans3: "אסור בהחלט",
          ans4: "לא",
          correctAnswer: 1,
          numAnswer: 4,
        },
        {
          Qtype: 3,
          title: "במה ואיזה מנועים יש בעגורן גשר?",
          ans1: "4 מנועים חשמליים",
          ans2: "ישנו רק מנוע 1",
          ans3: "יש 3 מנועים",
          ans4: "אין אף מנוע לעגורנים גשר",
          correctAnswer: 1,
          numAnswer: 4,
        },
      ],
    };
  },
  methods: {
    checkAnswer(event) {
      if (event.target.classList.contains("pulse-button-hover") && !this.clickeAnswer) {
        this.clickeAnswer = true;
        //בדיקה אם הכפתור הנלחץ הוא תשובה נכונה
        if (
          (this.questions[this.numQues].Qtype === 1 &&
            this.isInTheArray(
              this.questions[this.numQues].correctAnswer,
              event.target.id
            )) ||
          (this.questions[this.numQues].Qtype !== 1 &&
            String(event.target.id) ===
              String(this.questions[this.numQues].correctAnswer))
        ) {
          event.target.classList.add("correct");
          //בודק אם זאת שאלה עם תשובה אחת (שנכונה) או אם 3 תשובות שנלחצו ונכונות
          if (
            (this.questions[this.numQues].Qtype === 1 &&
              this.getNumCorrect() === 3) ||
            this.questions[this.numQues].Qtype !== 1
          ) {
            if(this.numQues === 3) {
              this.showFinish = true;
            }
            setTimeout(() => {
              for (
                let i = 1;
                i <= this.questions[this.numQues].numAnswer;
                i++
              ) {
                if (this.$refs[i].classList.contains("correct")) {
                  this.$refs[i].classList.remove("correct");
                }
                if (this.$refs[i].classList.contains("wrong")) {
                  this.$refs[i].classList.remove("wrong");
                }
              }
              
              if (this.numQues < 3) {
                this.numQues++;
              } else {                
                this.$emit("next-part");             
              }
              this.clickeAnswer = false;
            }, 1500);
          } else {
            this.clickeAnswer = false;
          }
        } else {
          event.target.classList.add("wrong");
          this.clickeAnswer = false;
        }
      }
    },
    isInTheArray(arr, currentId) {
      for (let i = 0; i < arr.length; i++) {
        if (String(arr[i]) === String(currentId)) {
          this.arrayChosenCorrect[i] = true;
          return true;
        }
      }
      return false;
    },
    getNumCorrect() {
      let counter = 0;
      for (let i = 0; i < 3; i++) {
        if (this.arrayChosenCorrect[i]) {
          counter++;
        }
      }
      return counter;
    },

    backToInfo() {
      this.$emit("back-to-info");
      this.$emit('hide-navbar', false);
    },

  },
};
</script>

<style scoped>
#american-questions {
  display: flex;
  z-index: 1;
  height: 100%;
  width: 100%;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.row {
  display: flex;
  margin: 5% 0% 5% 0%;
  justify-content: center;
}

.title-questionMultiple {
  font-size: 2.2rem;
}

.pulse-button-hover {
  background-color: #ffaf02;
  margin: auto;
  cursor: pointer;
  border: none;
  width: 10rem;
  height: 6.5rem;
  font-size: 1.4rem;
  color: #ffffff;
  border-radius: 2rem;
}

.pulse-button-hover:hover {
  animation: borderPulse 4000ms infinite ease-out, hoverShine 200ms;
}

@keyframes borderPulse {
  0% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255, 0.4),
      0px 0px 0px 0px rgba(255, 255, 255, 1);
  }

  100% {
    box-shadow: inset 0px 0px 0px 3px rgba(24, 24, 176, 0.2),
      0px 0px 0px 10px rgba(255, 255, 255, 0);
  }
}

@keyframes hoverShine {
  0% {
    background-image: linear-gradient(
      135deg,
      rgba(255, 255, 255, 0.4) 0%,
      rgba(255, 255, 255, 0) 50%,
      rgba(255, 255, 255, 0) 100%
    );
  }

  50% {
    background-image: linear-gradient(
      135deg,
      rgba(255, 255, 255, 0) 0%,
      rgba(255, 255, 255, 0.4) 50%,
      rgba(255, 255, 255, 0) 100%
    );
  }

  100% {
    background-image: linear-gradient(
      135deg,
      rgba(255, 255, 255, 0) 0%,
      rgba(255, 255, 255, 0) 50%,
      rgba(255, 255, 255, 0.4) 100%
    );
  }
}

.correct {
  background-color: green;
}

.wrong {
  background-color: rgb(176, 6, 6);
}

.div-mulQ {
  width: 40rem;
  background: #fff;
  border-radius: 3rem;
  box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
}

.second-instraction {
  color: #5f5a5a;
}

.moving-btn {
  z-index: 1;
  position: absolute;
  bottom: 2rem;
  width: 5rem;
  height: 3rem;
  font-size: 1rem;
  background-color: #8cd0ec;
  border: none;
  border-radius: 1.5rem;
  padding: 0; 
  /* Centering the text */
  display: flex;
  justify-content: center; 
  align-items: center; 
  text-align: center; 
  transition: background-color 0.3s ease;
  color: black;
  cursor: pointer;
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

@keyframes hoverShine {
  0% {
    background-image: linear-gradient(
      135deg,
      rgba(255, 255, 255, 0.4) 0%,
      rgba(255, 255, 255, 0) 50%,
      rgba(255, 255, 255, 0) 100%
    );
  }

  50% {
    background-image: linear-gradient(
      135deg,
      rgba(255, 255, 255, 0) 0%,
      rgba(255, 255, 255, 0.4) 50%,
      rgba(255, 255, 255, 0) 100%
    );
  }

  100% {
    background-image: linear-gradient(
      135deg,
      rgba(255, 255, 255, 0) 0%,
      rgba(255, 255, 255, 0) 50%,
      rgba(255, 255, 255, 0.4) 100%
    );
  }
}

.finish {
  background-color: #023047;
  padding: 7rem;
  border-radius: 1rem;
  position: absolute;
  color: white;
}

@media screen and (max-width: 600px) {
  .div-mulQ {
    width: 100vw;
    border-radius: 0rem;
  }

  #american-questions {
    height: 92vh;
  }
  
}
</style>
