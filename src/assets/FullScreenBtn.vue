<template>
    <button @click="toggleFullscreen" class="fullscreen-btn">
      ⛶ מסך מלא
    </button>
  </template>
  
  <script>
  export default {
    name: "fuul-screen-btn",
    methods: {
      toggleFullscreen() {
        const elem = document.documentElement; // the whole page
  
        if (!document.fullscreenElement) {
          if (elem.requestFullscreen) {
            elem.requestFullscreen();
          } else if (elem.webkitRequestFullscreen) { // Safari
            elem.webkitRequestFullscreen();
          } else if (elem.msRequestFullscreen) { // IE11
            elem.msRequestFullscreen();
          }
        } else {
          if (document.exitFullscreen) {
            document.exitFullscreen();
          } else if (document.webkitExitFullscreen) {
            document.webkitExitFullscreen();
          } else if (document.msExitFullscreen) {
            document.msExitFullscreen();
          }
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .fullscreen-btn {
    position: fixed;
    top: 10px;
    right: 10px;
    background: #333;
    color: white;
    border: none;
    padding: 8px 14px;
    cursor: pointer;
    z-index: 9999;
    border-radius: 4px;
    font-size: 14px;
  }
  .fullscreen-btn:hover {
    background: #555;
  }
  </style>
  