<template>
  <div id="summary-operation">
    <div class="info-container">

    </div>
  </div>
</template>

<script>
export default {
  name: "summary-operation",
  props: [""],
  data() {
    return {};
  },
  computed: {},
};
</script>

<style scoped>
#summary-operation {
 display: flex;
  color: white;
  height: 100%;
  width: 100vw;
  flex-direction: column;
    justify-content: center;
    align-items: center;
}

.info-container {
  background-color: #023047;
  border-radius: 1rem;
  width: 50rem;
  height: 30rem;
}
</style>
