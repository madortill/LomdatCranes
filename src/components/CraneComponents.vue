<template>
  <div id="crane-components">
    <p class="header fix-header" :class="showZoom? 'fade-out-animation' : ''">מרכיבים בעגורן</p>
    <object
      :class="showZoom ? 'with-zoom' : ''"
      class="img-crane"
      type="image/svg+xml"
      data="/media/theCraneInCraneComponents.svg"
    ></object>

    <div class="info-container" :class="showInfo? 'fade-in-animation' : ''" :style="{ '--bg-color': arrBgColors[numPart] }">
      <p class="header" >{{ arrInfo[numPart][0] }}</p>
      <p>{{ arrInfo[numPart][1] }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "crane-components",
  data() {
    return {
      showZoom: false,
      numPart: 0,
      arrBgColors: ['#E6BC4D','#F78C1E', '#2085AE'],
      arrInfo: [
        ['מפסקי גבול', 'לכל כננת חשמלית בעגורן יש מפסק גבול, המפסיק את פעולות המנוע בדיוק לפני סוף המהלך. תפקידו של המפסק למנוע נזק לעגורן או לציוד הסובב אותו. מפסק גבול נוסף שתפקידו להאט את מהירות הכננת כאשר הוא קרוב לסופה של קורה.'],
         [], []
      ],
      showInfo: false,
    };
  },
  mounted() {
    setTimeout(() => {
      this.showZoom = true;
      setTimeout(() => {
        this.showInfo = true;
      }, 3000);
    }, 1000); // The zoom effect is triggered after 700ms
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
  position: relative;
  z-index: -1;
  overflow: hidden ;  
}

.img-crane {
  width: 30rem; /* Set the initial size */
  margin-bottom: -1rem;
  position: relative;  /* Add position to make z-index work */
  transition: transform 3s ease-in, width 3s ease-in, margin-top 3s ease-in, margin-left 3s ease-in;
  z-index: -1;  /* Ensure z-index is applied */
}

.with-zoom {
  width: 280rem; /* Adjust width for zoom effect */
  margin-top: -176rem;
  margin-left: 190rem;
  /* position: relative; */
}

.header {
  font-size: 2.5rem;
  font-weight: bold;
}

.fix-header {
  margin-top: 8rem;
}

.fade-out-animation {
  animation: fadeOut 0.2s linear forwards;
}

@keyframes fadeOut {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    visibility: hidden;
  }
}

.info-container {
  position: absolute;
  background-color: var(--bg-color);
  width: 41rem;
  left:50%;
  transform: translateX(-43.7%);
  height: 23.2rem;
  top: 14.3rem;
  opacity: 0;
}

.fade-in-animation {
  animation: fadeIn 0.2s linear forwards;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
   
  }
}
@media screen and (max-width: 600px) {
  #crane-components {
    height: 91vh;
  }
  .with-zoom {
  width: 260rem; /* Adjust width for zoom effect */
  margin-top: -156rem;
  margin-left: 179rem;
  /* position: relative; */
}

.info-container {
    width: 30rem;
    height: 21.8rem;
    top: 21.3rem;
    transform: translateX(-50%);
}
}
</style>
