<template>
    <div id="app">
        <clouds-bg class="clouds-bg"></clouds-bg>
        <img class="bahadSymbol" src="../src/assets/media/bahadSymbol.png" alt="bahadSymbol"/>
        <img @click="toHomePage" v-if="part > 0" class="homeIcon" src="../src/assets/media/homeIcon.png" alt="homeIcon"/>
        <open-page :showSelection="showSelection" @to-study="showStartSign" v-if="part === 0"></open-page>
        <start-sign :partNum="partNum" :firstChosen="firstChosen" v-if="part === 1"></start-sign>
    </div>

</template>

<script>
import CloudsBg from './components/CloudsBg.vue';
import OpenPage from './components/OpenPage.vue';
import StartSign from './components/StartSign.vue';
export default {
        name: "app", 
        components: {
            OpenPage,
            StartSign,
            CloudsBg,
        },
        data() {
            return {
                part: 0,
                partNum: -1,
                firstChosen: null,
                showSelection: false,
            };
        },
        methods: {
            showStartSign (fChosen, studyPart) {
                this.partNum = studyPart;
                this.firstChosen = fChosen;
                this.part++;
            },
            toHomePage () {
                this.part--;
                this.showSelection = true;
            }
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
    background-color: #E0F2F4;
    /* display: grid; */

}

.bahadSymbol {
  width:4rem;
  position: absolute;
  top: 1rem;
  left: 1rem;
}

.homeIcon {
    position: absolute;
    right: 1rem;
    top: 1rem;
    width: 2.5rem;
    cursor: pointer; 
    z-index:4;
}

</style>
