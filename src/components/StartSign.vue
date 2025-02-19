<template>
    <div id="start-sign">
        <img class="start-sign-img" src="../../src/assets/media/StartSign.png" alt="startSign"/>
        <div v-if="firstChosen">
            <p>בחרת ב -</p>
            <p style="partOfLomda">{{arrPartTitle[partNum]}}</p>
            <p>אם תרצה לשנות את בחירתך אפשר ללחוץ על כפתור הבית</p>
            <p style="goodWord">בהצלחה!</p>
        </div>
        <div v-if="!firstChosen">
            <p>כל הכבוד סיימת את החלק ה{{arrFinishedPart[partNum-1]}}</p>
            <p>עכשיו נעבור לחלק ה{{ arrFinishedPart[partNum]}} של הלומדה</p>
            <p style="partOfLomda">{{arrPartTitle[partNum]}}</p>
            <p style="goodWord">בהצלחה!</p>
        </div>
        <div v-if="partNum === 0 && index === 1">
          <p>מטרות השיעור</p>
          <p>מטרת העל:</p>
          <p>מטרת הביניים:</p>
        </div>
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
            };
        },
        methods: {
          nextBoard(){
            this.$emit('toNextBoard');
            },
        },
    };
</script>

<style scoped>
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
    width: 40rem;
  }
</style>