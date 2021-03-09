<template>
  <div class="crease">
    <div class="row goalierow">
      <!-- <div class="col" /> -->
      <div class="col text-center">
        <div class="btn-group">
          <button
            ref="lineG"
            type="button"
            class="btn btn-outline-primary dropdown-toggle"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            Goalie
          </button>
          <div class="dropdown-menu">
            <span
              @click="setPlayer(goalie.name)"
              v-for="goalie in sortedGoalies"
              class="dropdown-item"
              href="#"
              :key="goalie.number"
              >{{ goalie.name }}
              <span class="badge badge-primary badge-pill">{{
                goalie.position
              }}</span></span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
  <hr class="red" />
</template>

<script>
import json from "../json/relics.json";
export default {
  name: "Goalies",
  data() {
    return {
      goalies: [],
      roster: json,
    };
  },
  methods: {
    setPlayer(playerName) {
      this.$refs.lineG.innerText = playerName;
    },
  },
  computed: {
    sortedGoalies() {
      function compare(a, b) {
        if (a.name < b.name) return -1;
        if (a.name > b.name) return 1;
        return 0;
      }
      return this.roster
        .filter((player) => {
          return player.type.toLowerCase().includes("goalie") && player.playing;
        })
        .sort(compare);
    },
  },
  mounted() {
    this.goalies = this.roster;
  },
};
</script>

<style>
.crease {
  height: 100px;
  width: 200px;
  border: 5px solid red;
  border-radius: 150px 150px 0 0;
  margin: auto;
}
.red {
  border: solid red;
  margin: -5px;
  /* display: inline-block; */
}
.goalierow {
  padding-top: 50px;
}
</style>
