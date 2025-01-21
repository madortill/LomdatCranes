<template>
    <div id="app">
        <open-page></open-page>
    </div>

</template>

<script>
import OpenPage from './components/OpenPage.vue';
export default {
        name: "app", 
        components: {
          OpenPage,
        },
        data() {
            return {};
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

.logo {
    max-width: 100px;
    left: 0;
    top: 0;
    position: absolute;
    margin-top: 1%;
    margin-left: 1%;
    z-index: 3;
}
</style>
