<template>
      <!-- <div id="container"> -->
      <!-- <div class="v-center"></div> -->
      <div class="book">
        <div class="first paper">
          <div class="page front contents">
            <div class="intro">
              <h1>כללי ברזל אותם עליך לדעת לפני הפעלת מנוף</h1>
            </div>
          </div>
          <div class="page back"></div>
        </div>
        <div class="second paper">
          <div class="page front contents">
            <!-- Static content or empty -->
            <div class="content">בתור חונכים, עלינו להבין מהם הרגלי הלמידה של הנחנך שלנו</div>
          </div>
          <div class="page back"></div>
        </div>
        <div class="third paper">
          <div class="page front contents">
            <!-- Static content or empty -->
            <div class="content">למה?  כדי להתאים את תהליך החניכה אליו ככל שניתן</div>
          </div>
          <div class="page back"></div>
        </div>
        <div class="side"></div>
        <div class="bottom"></div>
        <div class="shadow"></div>
      </div>
    <!-- </div> -->
</template>

<script>
export default {
  name: 'final-highlights',
  data() {
    return {

      pageStack: [], // Track page flips
      maxPages: 2, // Total number of pages
    };
  },
  mounted() {
    this.setupBookInteractions();
  },
  methods: {
    setupBookInteractions() {
      const pages = document.querySelectorAll(".paper");

      pages.forEach((page, index) => {
        const front = page.querySelector(".front");
        const back = page.querySelector(".back");

        if (front) {
          front.addEventListener("click", () => {
            const book = document.querySelector(".book");
            const isOpening = !page.classList.contains("open");

            if (isOpening) {
              if (this.pageStack.length < this.maxPages) {
                this.pageStack.push(page); // Save current page before flipping
                book.classList.add("open");
                page.classList.add("open");
              }
            } else {
              book.classList.remove("open");
              page.classList.remove("open");
            }
          });
        }

        if (back) {
          back.addEventListener("click", () => {
            const book = document.querySelector(".book");

            if (this.pageStack.length) {
              const lastPage = this.pageStack.pop(); // Get the last page
              book.classList.remove("open");
              lastPage.classList.remove("open");
            }
          });
        }
      });
    },
    // onSwitchPage() {
    //   this.$emit("add-green", this.componentName);
    // }
  }
};
</script>

<style scoped>



.text {
  font-size: 2rem;
  position: absolute;
  width: 70%;
  left: 50%;
  transform: translateX(-50%);
  top: 20rem;
  font-family: 'Heebo-light';
  color: #03045E;
  white-space: pre-line;
}

#container {
  /* width: 60%; */
  margin: 20px auto;
}

.v-center {
  display: inline-block;
  vertical-align: middle;
  height: 100%;
  width: 0;
}

.book {
  transform-style: preserve-3d;
  transform: rotateX(45deg) rotateY(0deg) rotateZ(-40deg);
  transition: transform 1s;
  position: absolute;
  left: 0;
  top: 12vh;;
  right: 13vw;;
  bottom:0%;
  margin: auto;
  width: 5vw; /* Reduced width */
  height: 15em; /* Reduced height */
  cursor: pointer;
}

.book .side {
  width: 2em; /* Reduced width */
  height: 25em; /* Reduced height */
  background: #b36060;
  position: absolute;
  left: -2em; /* Adjusted position */
  top: 0;
  transform-origin: 100% 100%;
  transform: rotateY(-90deg) rotateX(0deg);
}

.book .bottom {
  width: 15em; /* Reduced width */
  height: 2em; /* Reduced height */
  background: #e2e2e2;
  position: absolute;
  bottom: 0;
  left: 0;
  transform-origin: 100% 100%;
  transform: rotateX(90deg);
}
.book .page.front .contents {
  display: flex; /* or 'grid' for the Grid layout */
  justify-content: center; /* Center horizontally */
  align-items: center;     /* Center vertically */
  height: 100%;
  width: 100%;
  text-align: center;      /* Center text horizontally, optional */
}

.book .intro,
.book .content {
  margin: 0; /* Ensure no extra margins */
}

.book .second .content,
.book .third .content{
  font-size: 1.5rem !important; /* Force the font size to be applied */
}


.book.open {
  transform: rotateX(35deg) rotateY(0deg) rotateZ(-35deg);
}

.book .paper,
.book .shadow {
  width: 15em; /* Reduced width */
  height: 25em; /* Reduced height */
  position: absolute;
  top: 0;
  left: 0;
}

.book .shadow {
  background: transparent;
  transform: translateZ(-3em);
  box-shadow: -1em 1em 0px 0px #ccc3a9;
  z-index: 1;
}

.book .paper {
  transition: transform 1s, box-shadow 0.5s 0.2s;
  transform-origin: 0 50%;
  transform-style: preserve-3d;
}

.book .paper.open {
  box-shadow: 2.2em 1em 0px 0px #ccc3a9;
  transform: rotateX(0deg) rotateY(-180deg) rotateZ(0deg);
}

.book .paper .page.front {
  transition: transform 1s;
  transform-origin: 0 50%;
  backface-visibility: hidden;
  z-index: 2;
}

.book .page {
  width: 100%;
  height: 100%;
  position: absolute;
  transform: translateZ(0px);
}

.book .first .page {
  background: #ef9a9a;
}

.book .first .page.front:after {
  position: absolute;
  content: "";
  width: 50%;
  height: 100%;
  left: 0;
  top: 0;
  background: rgba(160, 115, 115, 0.1);
}

.book .paper .back {
  transition: transform 1s;
  transform-origin: 0 50%;
  background: #e1e1e1;
}

.book .first.paper .back {
  background: #ef9a9a;
}

.book .intro {
  position: absolute;
  width: 80%; /* Adjusted width */
  height: 80%; /* Adjusted height */
  border: 1em solid #eee;
  left: 0;
  top: 0;
  margin: auto;
}

.book .intro h2 {
  padding: 0.5em 0.5em;
  font-size: 3rem; /* Adjusted font size */
  color: #fff;
  word-break: break-all;
  text-align: left;
  letter-spacing: 5px;
}

.book .intro h1 {
  padding: 0.5em 0.25em;
  font-size: 3rem; /* Adjusted font size */
  color: #fff;
}

.book .paper:not(.first) .page {
  background: #f1f1f1;
  background-image: linear-gradient(
      90deg,
      transparent 40px,
      #abced4 40px,
      #abced4 42px,
      transparent 42px
    ),
    linear-gradient(#e1e1e1 0.1em, transparent 0.1em);
  background-size: 100% 1.5em;
}

.book .paper:not(.first) .back {
  background: #e1e1e1;
}

.book .open.second .back {
  transform: translateZ(-1px);
}

.book .open.third .back {
  transform: translateZ(-2px);
}

.book .paper.first {
  z-index: 8;
}

.book .paper.second {
  z-index: 7;
}

.book .paper.third {
  z-index: 6;
}

.book .paper.fourth {
  z-index: 5;
}

.book .paper.first .front {
  transform: translateZ(0.4px);
}

.book .paper.second .front {
  transform: translateZ(0.3px);
}

.book .paper.third .front {
  transform: translateZ(0.2px);
}

.book .paper.fourth .front {
  transform: translateZ(0.1px);
}

.book .second-page #vara-container {
  width: 100%;
  height: 100%;
  padding: 1em;
}

.book.open {
  transform: rotateX(35deg) rotateY(0deg) rotateZ(-35deg);
}

.book .paper.open {
  box-shadow: 2.2em 1em 0px 0px #ccc3a9;
  transform: rotateX(0deg) rotateY(-180deg) rotateZ(0deg);
}

.book .page.front {
  backface-visibility: hidden;
  transform: translateZ(0.4px);
}

.book .page.back {
  background: #e1e1e1;
}

#link {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #615858;
  letter-spacing: 2px;
  text-decoration: none;
}

@media (max-width: 700px) {
  .book {
    left: 50%;
  }
}

</style>
