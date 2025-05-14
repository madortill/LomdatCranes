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
      <div
        class="light-blue-circle"
        :class="showPhoneMenu ? 'pop-out-menu' : ''"
      >
        <img
          @click="showMenu"
          v-if="!showPhoneMenu"
          class="menu-icon"
          src="/media/phoneMenu.png"
          alt="menu-icon"
        />
        <div class="menu-container" v-if="showPhoneMenu">
          <p class="close-btn" @click="closeMenu">x</p>
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
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "navbar",
  props: ["part", "subjNum"],
  data() {
    return {
      showPhoneMenu: false,
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
    };
  },
  methods: {
    showMenu() {
      this.showPhoneMenu = true;
    },
    closeMenu() {
      this.showPhoneMenu = false;
    },
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

    nextSubPart() {
      this.subjNum++;
    },
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
  font-size: 1rem;
}

.phone-navbar {
  display: none;
  width: 100vw;
  height: 80vh;
}

.the-stripe-topic {
  display: flex;
  background-color: #023047;
  width: 100%;
  color: white;
  font-size: 1.8rem;
  font-weight: bold;
  align-items: center;
  height: 4.2rem;
  z-index: 2;
  position: relative;
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
  z-index: 3;
}

.pop-out-menu {
  width: 30rem;
  height: 80vh;
  z-index: 3;
  right: -7rem;
  top: -5rem;
  transition: all 1s;
}

.menu-icon {
  width: 3rem;
  /* pointer-events: auto; */
  z-index: 10;
}

.subj-text {
  margin-right: 7rem;
  font-size: 1.3rem;
}

.menu-container {
  height: 87%;
  width: 60%;
  position: relative;
  right: 1rem;
  top: 1rem;
  display: flex;
    flex-direction: column;
    align-items: center;
}

.close-btn {
  font-size: 3rem;
  position: absolute;
  right: 1.5rem;
  top: -2.5rem;
}


</style>
