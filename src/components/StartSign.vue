<template>
    <div id="start-sign">
        <img class="start-sign-img" src="../../src/assets/media/StartSign.png" alt="startSign"/>
        <div class="text-container" v-if="firstChosen">
            <p>בחרת ב -</p>
            <p class="partOfLomda">{{arrPartTitle[partNum]}}</p>
            <p>אם תרצה לשנות את בחירתך אפשר ללחוץ על כפתור הבית</p>
            <p class="goodWord">בהצלחה!</p>
        </div>
        <div class="text-container" v-if="!firstChosen">
            <p>כל הכבוד סיימת את החלק ה{{arrFinishedPart[partNum-1]}}</p>
            <p>עכשיו נעבור לחלק ה{{ arrFinishedPart[partNum]}} של הלומדה</p>
            <p class="partOfLomda">{{arrPartTitle[partNum]}}</p>
            <p class="goodWord">בהצלחה!</p>
        </div>
        <div class="text-container" v-if="partNum === 0 && index === 1">
          <p>מטרות השיעור</p>
          <p>מטרת העל:</p>
          <p>מטרת הביניים:</p>
        </div>
        <div v-if="partNum > 0 && firstChosen && showWarning">
          <div class="shadow"></div>
          <div class="warning-container">
            <p>שימו לב!</p>
            <p>אם לא תתחיל מתחילת הלומדה אז ציונך לא יעלה למפקדיך</p>
          </div>
        </div>
       
       <button class="next-btn">הבא</button>
        
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
              index: 0,
              showWarning: true,
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
          nextBoard(){
            this.$emit('toNextBoard');
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
  .goodWord {
      color: #8CD0EC;
      font-size: 1.5rem;
  }

  .partOfLomda {
    color: #FFB703;
    font-size: 2.5rem;
    margin: 0rem;
  }

  .start-sign-img {
    width: 60rem;
    height: 90%;
    z-index: 0;
    margin-bottom: -3rem;
    margin-right:1rem;
    margin-left:1rem;
  }

  .text-container {
    position: absolute;
    top:50%;
    left:50%;
    transform: translate(-50%, -50%);
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
    top:50%;
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
  }

  .next-btn {
    background-color: #8CD0EC;
    border-radius: 2rem;
    border-color:  #8CD0EC;
  }
</style>