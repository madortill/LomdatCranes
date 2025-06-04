<template>
    <div id="exam-results">
    </div>
  </template>
  
  <script>
  export default {
    name: "exam-results",
    props:[],
    data() {
      return {
      };
    },
    methods: {

    }
  };
  </script>
  
  
    
    <style scoped>
    #exam-results {
        width: 100vw;
    height: 100vh;
    display: flex;
    z-index: 1;
    }
  
    @media screen and (max-width: 600px) {
        #exam-results {
      width: 100vw;
      height: 91vh;
    }
  }
    </style>
    