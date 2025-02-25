<template>
    <div id="info-screen">
        <navbar :part="navPart"></navbar>
        <definition></definition>
    </div>
</template>

<script>
import Definition from './Definition.vue';
import Navbar from './Navbar.vue';
    export default {
        name: "info-screen",
        components: { Definition, Navbar },
        props: ["navPart"],
        data() {
            return {
                // part: 1,
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
        justify-content: center;
    }
</style>