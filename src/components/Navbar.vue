<template>
  <div id="navbar">
    <div class="computer-navbar">
      <div v-for="(subj, index) in theRightArr" :key="index">
        <p
          :class="{
            subject: index !== 0,
            'main-subj': index === 0,
            'now-subject': subjNum === index,
          }"
        >
          {{ subj }}
        </p>
      </div>
    </div>

    <div class="phone-navbar">
      <div class="the-stripe-topic">
        <p class="subj-text">{{ theRightArr[subjNum] }}</p>
      </div>
      <div @click="showMenu" class="light-blue-circle">
        <img
          class="menu-icon"
          src="../../src/assets/media/phoneMenu.png"
          alt="menu-icon"
        />
      </div>
    </div>
    <div class="hidden-menu-container">

    </div>
  </div>
</template>

<script>
export default {
  name: "navbar",
  props: ["part"],
  data() {
    return {
      arr1: [
        "רקע כללי",
        "הגדרה",
        "בטיחות",
        "סוגי עגורנים",
        "כננות",
        "מרכיבים בעגורן",
        "תוספות",
        "מערכת החשמל",
        "שיטות פיקוד",
      ],
      arr2: [
        "תפעול",
        "פתיחת זרם חשמל ראשי",
        "הוצאת השלט",
        "שחרור פטריית חירום",
        "שחרור העגורן מנקודת האחסון",
      ],
      subjNum: 1,
    };
  },
  computed: {
    theRightArr() {
      // איחוד שני המערכים לפי ה-part שהתקבל
      if (this.part === 0) {
        return this.arr1;
      } else if (this.part === 1) {
        return this.arr2;
      }
      return []; // במקרה שאין תוצאה תוחזר מערך ריק
    },
    showMenu() {

    }
  },
};
</script>

<style scoped>
#navbar {
  width: 100vw;
  height: 100vh;
  margin-top: 0rem;
  display: flex;
  justify-content: center;
  position: absolute;
}

.phone-navbar {
  display: none;
  width: 100vw;
  height: 5rem;
}

.the-stripe-topic {
  display: flex;
  background-color: #023047;
  width: 100%;
  height: 100%;
  color: white;
  font-size: 2rem;
  font-weight: bold;
  align-items: center;
}

.computer-navbar {
  width: 65rem;
  height: 4rem;
  border-radius: 1rem;
  margin-top: 1rem;
  z-index: 2;
  background-color: #023047;
  color: white;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  align-items: center;
    margin-left: 6rem;
    margin-right: 6rem;
}

@media screen and (max-width: 600px) {
  .computer-navbar {
    display: none;
  }

  .phone-navbar {
    display: block;
  }
}

.subject {
  /* transition: background-color 0.3s ease; */
  border-radius: 0.52rem;
  padding: 0.5rem;
}

.now-subject {
  background-color: #ffb703;
  color: #023047;
}

.main-subj {
  font-weight: 500;
  font-size: 2rem;
}

.light-blue-circle {
  background-color: #8cd0ec;
  border-radius: 100%;
  width: 8rem;
  height: 8rem;
  position: absolute;
  right: -2rem;
  top: -2rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.menu-icon {
  width: 3rem;
}

.subj-text {
  margin-right: 7rem;
}

.hidden-menu-container {
  background-color: #8cd0ec;
  height: 100vh;
  width: 20rem;
  position: absolute;
  z-index: 2;
  right: 0rem;
  display: none;
}
</style>
