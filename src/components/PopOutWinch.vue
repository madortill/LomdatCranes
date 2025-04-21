<template>
  <div id="pop-out-winch">
    <p @click="closeWindow" class="close-info">X</p>

    <p class="header">{{ title }}</p>
    <p >{{ explainArr[indexTypes] }}</p>
    <button v-if="showBackBtn" class="moving-btn back-btn">חזור</button>
    <button v-if="showNextBtn" class="moving-btn next-btn">הבא</button>
  </div>
</template>

<script>
export default {
  name: "pop-out-winch",
  props: ["title", "indexTypes"],
  data() {
    return {
        explainArr: [
            'מופעלת באופן מכאני ומיועדת לכבל לב חבל',
            'מופעלת באופן מכאני ומיועדת לשרשרת הרמה',
            'מופעלת באמצעות מנוע חשמלי המיועד לשרשרת הרמה',
            'מופעלת באמצעות מנוע חשמלי המיועד לכבל לב חבל',
        ],
        showNextBtn: false,
        showBackBtn: false,
    };
  },
  methods: {
    closeWindow() {
        this.$emit('close-pop-out');
    }
  },
  computed: {
   
  },
};
</script>

<style scoped>
#pop-out-winch {
  /* background-color: #023047; */
  background-color: white;
  /* padding: 1rem; */
  border-radius: 1rem;
  position: absolute;
  /* color: white; */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 20rem;
  width: 30rem;
}

.header {
  font-size: 2rem;
  font-weight: bold;
  /* padding: 2rem; */
}

.close-info {
  /* margin-left: 22rem; */
  cursor: pointer;
  font-size: 1.8rem;
  position: absolute;
  right: 1rem;
  top:-1rem;
  /* z-index: 30; */
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
  padding: 0; /* Remove padding to ensure centering works properly */
  /* Centering the text */
  display: flex;
  justify-content: center; /* Horizontally centers the text */
  align-items: center; /* Vertically centers the text */
  text-align: center; /* Ensures the text is centered if multiline */
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

@media screen and (max-width: 700px) {
}
</style>
