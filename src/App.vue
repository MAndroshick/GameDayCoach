<template>
  <!-- <Rink /> -->
  <Lines team="Relics" />
</template>

<script>
import Lines from "./components/Lines.vue";
// import Rink from "./components/Rink.vue";

export default {
  name: "App",
  components: {
    Lines,
    // Rink,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  /* color: #2c3e50; */
  /* margin-top: 60px; */
}
</style>
