<template>
    <div id="app">
        <img class="bahadSymbol" src="../src/assets/media/bahadSymbol.png" alt="bahadSymbol"/>
        <img src="../src/assets/media/homeIcon.png" alt="homeIcon"/>
        <open-page v-if="part === 0"></open-page>
        <start-sign v-if="part === 10"></start-sign>
    </div>

</template>

<script>
import OpenPage from './components/OpenPage.vue';
import StartSign from './components/StartSign.vue';
export default {
        name: "app", 
        components: {
            OpenPage,
            StartSign,
        },
        data() {
            return {
                part: 0,
            };
        },
        methods: {

        },
    };
</script>

<style >
@font-face {
    font-family: 'Heebo';
    src: url('@/assets/fonts/heebo.regular.ttf');
}

@font-face {
    font-family: 'Heebo-Bold';
    src: url('@/assets/fonts/heebo.black.ttf');
}

* {
    overflow: hidden;
    font-family: 'Heebo';
}


:root {
    font-size: calc(10px + 0.5vw)
}

body {
    margin: 0;
    direction: rtl;
    background-color: #F2F2F2;
}

#app {
    font-family: 'Heebo';
    width: 100vw;
    height: 100vh;
    position: relative;
    text-align: center;
}

.bahadSymbol {
  width:4rem;
  position: absolute;
  top: 1rem;
  left: 1rem;
}
</style>
