<template>
  <div id="command-method">
    <div class="pop-out">
      <p class="header">{{theInfo[0][partCommadMethod] }}</p>
      <p v-if="partCommadMethod === 0" >{{theInfo[cloudObject.num][0] }}</p>
      <img class="command-img" :class="cloudObject.num === 2 ? 'fix-scale' : ''" v-if="partCommadMethod=== 0" :src="getImage(cloudObject.num)"/> 
      <div v-if="partCommadMethod === 1">
        <p  v-for="(i,index) in theInfo" :key="index">{{theInfo[cloudObject.num][index +1] }}</p>
      </div>
      
      
      <p v-if="partCommadMethod === 0" @click="nextPart(true)" class="moving-btn next-btn">הבא</p>
      <p v-if="partCommadMethod === 1" @click="nextPart(false)" class="moving-btn back-btn">חזור</p>
      <p v-if="partCommadMethod === 1" class="moving-btn next-btn" @click="finishedTheMethod">אוקיי</p>
    </div>
    <div class="cloud" :class="`cloud${cloudObject.num}`">
      <p
        :class="
          cloudObject.num === 1 ||
          cloudObject.num === 4 ||
          cloudObject.num === 5
            ? 'title' + cloudObject.num
            : ''
        "
        class="cloud-text"
      >
        {{ cloudObject.text }}
      </p>
      <img class="cloud-img" :src="cloudObject.src" alt="cloud img" />
    </div>
  </div>
</template>

<script>
export default {
  name: "command-method",
  props: ["cloudObject"],
  data() {
    return {
      theInfo: [
        ["מדוע נקראת כך?", "איך עובדת שיטת הפיקוד?"],
        [
          "מכיוון שהידית מקובעת ישירות לקורה ואינה ניידת לאורך העגורן.",
          "בשיטה זו תלויה ידית הפיקוד באופן קבוע על הקורה העליונה. המפעיל אינו יכול ללוות את המטען ולתמוך בו.",
          "שיטה זו מתאימה לעגורנים בהם יש צורך לשמור על מרחק ביטחון מהמטען או מאזור העבודה.",
        ],
        [
          "מכיוון שהמפעיל שולט בעגורן על ידי שלט אלחוטי.",
          "בשיטה זו הפעלת העגורן נעשית על ידי שידור אלחוטי.",
          "מה שמאפשר למפעיל להיות בכל טווח העגורן ומצדדיו.",
        ],
        ["מכיוון שהידית נעה על מסילה והיא ניידת לאורך העגורן.",
          "בשיטה זו הידית תלויה על כבל הפיקוד הנע על מסילה נפרדת לאורך הקורה.",
          "למפעיל יש אפשרות לעמוד במרחק ביטחון מהמטען ולהוביל אותו מעל חפצים או מכשולים."
        ],
        [
          "מכיוון שהידית מקובעת ישירות לכננת.",
          "בשיטה זו כבל ידית הפיקוד מחובר קבוע לכננת ונע איתה לאורך הקורה העליונה.",
          "המפעיל תמיד בקרבת המטען ויש באפשרותו ללוות אותו ולתמוך בו.",
        ],
        [
          "מכיוון שהמפעיל יושב בתוך תא פיקוד חיצוני.",
          "בשיטה זו משתמשים בעגורנים מהירים יחסית או במצב אשר למפעיל אין אפשרות להלך על המשטח. המפעיל עצמו יושב בתוך תא ופעיל את העגורן מתוכו.",
          "תא הפיקוד יכול להיות מחובר לקורה העליונה או בצמוד לדפנות העגורן.",
        ],
      ],
      titlesInElectricalSystemArr: ["הסעה", "פיקוד", "חשמל"],
      partCommadMethod: 0,
    };
  },
  methods: {
    getImage(num) {
      // Determine the base URL (for local and production)
      const basePath =
        process.env.NODE_ENV === "production" ? "/LomdatCranes/" : "/";
      return `${basePath}media/commandMethod/command${num}.png`; // Static path to the images in the public folder
    },

    finishedTheMethod() {
      this.$emit("finished-method", false);
    },
    nextPart(isNext) {
        if(isNext) {
            this.partCommadMethod++;
        } else{
            this.partCommadMethod--;
        }
        
    }
  },
  computed: {},
};
</script>

<style scoped>
#command-method {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.command-img {
  background-color: white;
  height: 10rem;
  width: 17rem;
}

.fix-scale {
  width: 5rem;
}

.pop-out {
  background-color: #023047;
  border-radius: 1rem;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -35%);
  height: 27rem;
  width: 55%;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: white;
  justify-content: center;
}

.header {
  font-size: 2rem;
  font-weight: bold;
  margin-top: 1rem;
}

.moving-btn {
  z-index: 1;
  position: absolute;
  bottom: 1rem;
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
  background-color: #145575;
  color: white;
}

.next-btn {
    left: 2rem;
}

.back-btn {
    right: 2rem;
}

.cloud {
  position: absolute;
  top: 9rem;
  right: 11rem;
  height: 10rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.cloud-text {
  position: relative;
  z-index: 3;
  width: 11rem;
  margin-top: 3rem;
  pointer-events: none;
  font-weight: bold;
  font-size: 1.3rem;
}

.cloud-img {
  z-index: 2;
  position: absolute;
  width: 100%;
  right: 0rem;
  top: 50%;
  transform: translateY(-50%);
}

.title1 {
  margin-left: 4rem;
}

.title4 {
  margin-right: 2rem;
}

.title5 {
  margin-right: 4rem;
}

.cloud1 {
  width: 21rem;
}

.cloud2 {
  width: 19rem;
}

.cloud3 {
  width: 16rem;
}

.cloud4 {
  width: 18rem;
}

.cloud5 {
  width: 24rem;
}


@media screen and (max-width: 1400px) {
  .cloud {
    top: 15rem;
  }
}

@media screen and (max-width: 700px) {
  .pop-out {
    height: 33rem;
    width: 90%;
  }

  .header {
    margin-top: 3rem;
  }
  
  .cloud {
    top: 12rem;
    right: auto;
  }
}
</style>
