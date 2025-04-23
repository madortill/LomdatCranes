<template>
    <div id="safety-rules">
      <div
        v-for="(item, index) in arrayImgFront"
        :key="index"
        :class="['flip-card', this.onStart]"
      >
        <div class="flip-card-inner">
          <div @mouseover="hoverCardsCounter(index)"
            class="flip-card-front" 
            :style="{ '--dynamic-color': frontColorArr[index] }"
          >
            <img :src="src(item)" class="imgFront" />
            <p class="text-front">{{ arrayFront[index] }}</p>
          </div>
          <div class="flip-card-back" :style="{ '--dynamic-color': frontColorArr[index]}">
            <p class="textBack">{{ arrayBack[index] }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "info-screen",
    props: ["chosenCourse"],
    data() {
      return {
        arrayBack: [
          'בדיקה כי העגורן ביצע טיפול/בדיקה תקופתית, בנוסף יש לבדוק כי לעגורן קיים תסקיר מהנדס שנתי.',
          'יש לבדוק כי לאביזרי ההרמה יש תסקיר מבוחן מצהר"ם מוסמך שמעיד על כשירות האביזרים.',
          `על המפעיל להיות בוגר קורס עגורן ${this.chosenCourse} בבה"ד 20 ובעל תעודת מפעיל מנוף בתוקף. בנוסף יש לוודא כי הפעיל בקיא בהפעלת העגורן.`,
          'יש לוודא עבודה על פי הוראות קטנא"ר, כגון מתיחה ראשית לאתר חיבור אביזרי הרמה, עבודה עם ציוד מיגון מתאים כגון כפפות, קסדה ואפוד זוהר ועוד.',
        ],
        arrayFront: [
          "כשירות המנוף",
          "כשירות האביזרים",
          "כשירות המפעיל",
          "עבודה על פי הוראות",
        ],
        arrayImgFront: [
          "flipCard4.png",
          "flipCard3.png",
          "flipCard2.png",
          "flipCard1.png",
        ],
        frontColorArr: [
          '#F88C01',
          '#FFAF02',
          '#8CD0EC',
          '#1E85AE',
        ],
        onStart: "start",
        hoveredCards: [-1,-1,-1,-1],
        counterHovered: 0,
        showNextBtn: false,
      };
    },
    methods: {
      src(name) {
        return new URL(`../assets/media/flipCards/${name}`, import.meta.url).href;
      },
      hoverCardsCounter(index) {
        if(this.hoveredCards[index] === -1) {
          this.hoveredCards[index] = index;
          this.counterHovered++;
        }
        if(this.counterHovered === 4 && !this.showNextBtn) {
          this.$emit('showNextBtn');
          this.showNextBtn = true;
        }
        
      }
    },
    mounted() {
      setTimeout(() => {
        this.onStart = "off";
      }, 200);
    },
  };
  </script>
  
  <style scoped>
  #safety-rules {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    height: 16rem;
    width: 50rem;
    flex-direction: row;
    justify-content: space-evenly;
  }
  
  .flip-card {
    background-color: transparent;
    width: 10rem;
    height: 10rem;
    margin: 1rem;
  }
  
  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
  }
  
  .flip-card:hover .flip-card-front,
  .flip-card.start .flip-card-front {
    transform: rotateY(180deg);
  }
  
  .flip-card:hover .flip-card-back,
  .flip-card.start .flip-card-back {
    transform: rotateY(360deg);
  }
  
  .flip-card-front,
  .flip-card-back {
    transition: transform 0.6s;
    transform-style: preserve-3d;
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
  }
  
  .flip-card-front {
    background-color: var(--dynamic-color);
    border-radius: 30px;
    color: black;
  }
  
  .flip-card-back {
    background-color:white;
    border-radius: 30px;
    color: rgb(84, 82, 82);
    transform: rotateY(180deg);
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .imgFront {
    width: 5rem;
    position: absolute;
    top: -0.1rem;
  }
  
  .textBack {
    padding: 5%;
    font-size: 0.9rem;
  }
  
  .text-front {
    font-size: 1.4rem;
    position: absolute;
    bottom: 0rem;
    text-align: right;
    right: 1rem;
    color: white;
  }

  @media screen and (max-width: 700px){
    #safety-rules {
      height: 25rem;
      display: flex;
    /* width: 50rem; */
    flex-direction: column;
    align-content: center;
    flex-wrap: wrap;
    }

    .textBack {
    padding: 3%;
    font-size: 1rem;
  }

  .flip-card-front {
    border-radius: 1rem;
  }
  
  .flip-card-back {
    border-radius: 1rem;
  }

  .flip-card {
    background-color: transparent;
    width: 11rem;
    height: 11rem;
    margin: 0.4rem;
  }

  .imgFront {
    width: 6rem;
  }
  
  
  }
  </style>
  