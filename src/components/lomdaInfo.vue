<template>
  <div id="lomda-info">
    <div class="info-container">
      <p @click="closeInfo" class="close-info">X</p>
      <ul class="info-list">
        <li class="info" v-for="(subTitle, title) in infoObject" :key="title">
          <span class="info-title">{{ title }}</span
          ><br />
          <span>{{ subTitle }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "lomda-info",
  data() {
    return {
      infoObject: {
        "מפתחת לומדה ראשית:": 'רב"ט דני שריקי',
        "גרפיקאית:": 'רב"ט קריסטינה ברחטוב, רב"ט דני שריקי',
        "מומחה תוכן:": 'רס"ר יוחאי עזרא',
        'רמ"ד טי"ל:': 'רס"מ שלומי אוגרן',
        "גרסה:": "ינואר 2025",
      },
    };
  },
  methods: {
    closeInfo() {
        this.$emit('hide-info');
    }
  },
};
</script>

<style scoped>
#lomda-info {
    width: 100vw;
    height: 100vh;
    z-index: 3;
    display: flex;
    justify-content: center;
    align-items: center;
}
.info-container {
  background-color: white;
  color: #023047;
  border-radius: 2rem;
  width: 27rem;
  height: 27rem;
  animation: windowShow 0.2s linear forwards;
  font-size: 1.5rem;
}

.info-list {
  display: flex;
  width: 100%;
  margin-top: -3rem;
  padding: 0%;
  flex-direction: column;
}

.info-title {
  font-weight: bold;
}

.info {
  margin-bottom: 1.2rem;
}

.close-info {
  margin-left: 22rem;
  cursor: pointer;
  font-size: 1.8rem;
  /* z-index: 30; */
}

@keyframes windowShow {
  0% {
    height: 25rem;
    width: 25rem;
    font-size: 1rem;
  }
  100% {
    height: 27rem;
    width: 27rem;
    font-size: 1.2rem;
  }
}
</style>
