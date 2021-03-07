<template>
  <div class="faceoff">
    <!-- <hr class="red" /> -->
    <img alt="Vue logo" :src="require(`@/assets/${team}.png`)" />
  </div>
  <div class="lines">
    <Skaters />
    <Goalies />
  </div>
</template>

<script>
import Goalies from "./Goalies";
import Skaters from "./Skaters";
export default {
  name: "Lines",
  components: {
    Goalies,
    Skaters,
  },
  props: {
    team: String,
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
