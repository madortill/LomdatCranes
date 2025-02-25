<template>
    <div id="navbar">
        <div v-for="(subj, index) in theRightArr" :key="index">
            <p :class="{'subject': index !== 0, 'main-subj': index === 0, 'now-subject': subjNum === index}">{{ subj }}</p>
        </div> 
    </div>
</template>

<script>
export default {
    name: "navbar",
    props: ["part"],
    data() {
        return {
            arr1: ['רקע כללי', 'הגדרה', 'בטיחות', 'סוגי עגורנים', 'כננות', 'מרכיבים בעגורן', 'תוספות', 'מערכת החשמל', 'שיטות פיקוד'],
            arr2: ['תפעול', 'פתיחת זרם חשמל ראשי', 'הוצאת השלט', 'שחרור פטריית חירום', 'שחרור העגורן מנקודת האחסון'],
            subjNum: 1,
        };
    },
    computed: {
        theRightArr() {
            // איחוד שני המערכים לפי ה-part שהתקבל
            if (this.part === 0) {
                return this.arr1;
            } else if (this.part === 1) {
                return this.arr2;
            }
            return []; // במקרה שאין תוצאה תוחזר מערך ריק
        }
    }
};
</script>

<style scoped>
    #navbar {
        width: 75rem;
        height: 4rem;
        border-radius: 1rem;
        margin-top: 1rem;        
        z-index: 2;
        background-color: #023047;
        color: white;
        display:flex;
        justify-content: space-evenly;
        align-items: center;
    }

    .subject {
        /* transition: background-color 0.3s ease; */
        border-radius: 0.52rem;
        padding: 0.5rem;
        
    }

    .now-subject {
        background-color: #FFB703;        
        color:#023047;
    }

    .main-subj {
        font-weight: 500;
        font-size: 2rem;
    }
</style>
