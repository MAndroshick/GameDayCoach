<template>
  <h1 class="text-center">2020-2021 Relics Fall/Winter</h1>
  <div class="progress">
    <div
      class="progress-bar progress-bar-striped progress-bar-animated"
      role="progressbar"
      aria-valuenow="13"
      aria-valuemin="0"
      aria-valuemax="20"
      style="width: 65%"
    ></div>
    <div
      class="progress-bar progress-bar-striped progress-bar-animated bg-danger"
      role="progressbar"
      style="width: 15%"
      aria-valuenow="3"
      aria-valuemin="0"
      aria-valuemax="20"
    ></div>
  </div>
  <div class="lines">
    <Skaters team="Relics" />
    <!-- <Goalies /> -->
  </div>
</template>

<script>
// import Goalies from "./Goalies";
import Skaters from "./Skaters";
export default {
  name: "Lines",
  components: {
    Skaters,
  },
  data() {
    return {
      players: Number,
      lines: [],
    };
  },
  methods: {
    something() {},
  },
  mounted() {
    this.players = 10;
  },
};
</script>

<style scoped>
.circle {
  height: 200px;
  width: 200px;
  border-radius: 50%;
  border: 5px solid red;
  margin: auto;
  position: relative;
}
img {
  height: 200px;
  width: 200px;
  border-radius: 50%;
  border: 10px solid black;
}
.faceoff,
.offense,
.defense {
  padding-block: 50px;
  text-align: center;
}
</style>
