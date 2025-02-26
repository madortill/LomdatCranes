<template>
    <div id="info-screen">
        <navbar :part="navPart"></navbar>
        <info-hanging-board :section="infoHangingPart"></info-hanging-board>
    </div>
</template>

<script>
import InfoHangingBoard from './InfoHangingBoard.vue';
import Navbar from './Navbar.vue';
    export default {
        name: "info-screen",
        components: { Navbar, InfoHangingBoard },
        props: ["navPart"],
        data() {
            return {
                Infopart: 1,
                infoHangingPart: 0,
            };
        },
    };  
</script>

<style scoped>
    #info-screen {
        z-index: 7;
        width: 100vw;
        height: 100vh;
        display: flex;
        align-items: center;
        flex-direction: column;
    }
</style>