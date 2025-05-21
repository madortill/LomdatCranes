<template>
  <div id="container-part-winch">
    <div
      @click="showInfo(item)"
      :class="item.clickedItem ? 'height-after-click' : 'height-before-click'"
      class="part-of-winch"
      :style="{ backgroundColor: item.color }"
      v-for="(item, index) in infoArr[indexInfoArr]"
      :key="index"
    >
      <p class="header">{{ item.header }}</p>
      <p class="info" v-if="item.clickedItem">{{ item.info }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "container-part-winch",
  props: ["indexInfoArr"],
  data() {
    return {
      infoArr: [
        [
          {
            header: "גוף הכננת",
            color: "#F88C01",
            info: "שרשרת הרמה המיועדת לשאת משקלים שונים",
            clickedItem: false,
          },
          {
            header: "גלגל שיניים",
            color: "#FFAF02",
            info: "מותאם לשרשרת ההרמה של הכננת",
            clickedItem: false,
          },
          {
            header: "מיכל איסוף שרשרת",
            color: "#8CD0EC",
            info: "מיועד לאחסון השרשרת בזמן שלא עובדים עם העגורן",
            clickedItem: false,
          },
          {
            header: "קרס",
            color: "#1E85AE",
            info: "מחובר לשרשרת ההרמה על מנת להתחבר למכלולים השונים",
            clickedItem: false,
          },
        ],
        [
          {
            header: "מתנע (סטרטר)",
            color: "#F88C01",
            info: "האחראי על התנעת הכננת מכיוון שהיא חשמלית",
            clickedItem: false,
          },
          {
            header: "מנוע חשמלי",
            color: "#FFAF02",
            info: "מנוע האחראי על תזוזת הכננת אחורה וקדימה / הרמה והורדת הכבל",
            clickedItem: false,
          },
          {
            header: "תוף כננת",
            color: "#FFD169",
            info: "שעליו מתלפף הכבל",
            clickedItem: false,
          },
          {
            header: "ציר תנועה",
            color: "#8CD0EC",
            info: "הציר שעליו נעה הכננת",
            clickedItem: false,
          },
          {
            header: "מערכות הפחתה",
            color: "#1E85AE",
            info: "מערכת שיכולה לשנות את מהירות הכננת",
            clickedItem: false,
          },
        ],
      ],
    };
  },
  methods: {
    showInfo(item) {
      item.clickedItem = true;
      if(this.isAllBeenClicked()) {
        this.$emit('finish-learning');
      }
    },
    //checks if all the items of winch has been clicked
    isAllBeenClicked() {
      for (let i = 0; i < this.infoArr[this.indexInfoArr].length; i++) {
        if (!this.infoArr[this.indexInfoArr][i].clickedItem) {
         return false;
        }
      }
      return true;
    },
  },
  computed: {},
};
</script>

<style scoped>
#container-part-winch {
  width: 100%;
  height: 60%;
  display: flex;
  justify-content: space-evenly;
  margin-top: 0rem;
}

.part-of-winch {
  /* margin: auto; */
  cursor: pointer;
  /* border: none; */
  width: 6.4rem;
  color: #ffffff;
  border-radius: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  transition: height 0.3s ease;
  /* overflow: hidden; */
}

.height-before-click {
  height: 5rem;
}

.height-after-click {
  height: 12rem;
  justify-content: flex-start;
}

.header {
  font-size: 1.1rem;
  font-weight: bold;
  margin-top: 0.8rem;
  /* margin-bottom: 1rem; */
}

.info {
  margin-top: 0rem;
  font-size: 1rem;
}

@media screen and (max-width: 700px) {
  .height-after-click {
    height: 13.8rem;
}

#container-part-winch {
  margin-top: -0.6rem;
}
.part-of-winch {
padding: 0.1rem;
  width: 5.6rem;
}

.info {
  margin-top: -0.6rem;
}

}
</style>
