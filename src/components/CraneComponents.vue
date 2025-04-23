<template>
    <div id="crane-components">
        <p class="header">מרכיבים בעגורן</p>
        <img class="img-crane" src="/media/theCraneInCraneComponents.svg" alt="crane"/>
    </div>
  </template>
  
  <script>
  export default {
    name: "crane-components",
    // props: ["chosenCourse"],
    data() {
      return {
     
      };
    },
    methods: {

    },

  };
  </script>
  
  <style scoped>
#crane-components {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;
}

.img-crane {
    width: 30rem;
    margin-bottom: -2.5rem;
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
  /* padding: 2rem; */
  margin-top: 8rem;
}
  @media screen and (max-width: 600px){
    #crane-components {
 
    height: 91vh;
   
}
  
  }
  </style>
  