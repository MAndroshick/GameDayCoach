<template>
  <div class="row">
    <div class="col-10">
      <div class="faceoff">
        <img alt="Vue logo" :src="require(`@/assets/${team}.png`)" />
      </div>
      <div class="row">
        <div class="col text-center">
          <button class="btn btn-primary">Set Lines</button>
        </div>
        <div class="col text-center">
          <button class="btn btn-danger">Clear</button>
        </div>
      </div>
      <div class="line">
        <hr class="red" />
      </div>
      <div id="lines">
        <div class="row" v-for="index in 4" :key="index">
          <div
            v-for="position in forwardPositions"
            :key="position"
            class="col text-center"
          >
            <div class="btn-group">
              <button
                :ref="'line' + index + position.abbr"
                type="button"
                class="btn btn-outline-primary dropdown-toggle"
                data-toggle="dropdown"
                aria-haspopup="true"
                aria-expanded="false"
              >
                {{ position.label }}
              </button>
              <div class="dropdown-menu">
                <span
                  @click="setPlayer(forward.name, index + position.abbr)"
                  v-for="forward in sortedForwards"
                  class="dropdown-item"
                  :key="forward.number"
                  >{{ forward.name }}
                  <span style="float:right" class="badge badge-dark">{{
                    forward.totalG
                  }}</span>
                  <span style="float:right" class="badge badge-danger">{{
                    forward.lastG
                  }}</span>
                  <span style="float:right" class="badge badge-primary">{{
                    forward.position
                  }}</span></span
                >
                <div class="dropdown-divider"></div>
                <span
                  @click="setPlayer(defenseman.name, index + position.abbr)"
                  v-for="defenseman in sortedDefense"
                  class="dropdown-item"
                  :key="defenseman.number"
                  >{{ defenseman.name }}
                  <span style="float:right" class="badge badge-dark">{{
                    defenseman.totalG
                  }}</span>
                  <span style="float:right" class="badge badge-danger">{{
                    defenseman.lastG
                  }}</span>
                  <span style="float:right" class="badge badge-primary">{{
                    defenseman.position
                  }}</span>
                </span>
              </div>
            </div>
          </div>
        </div>
        <hr class="blue" />
        <div class="row" v-for="index in 3" :key="index">
          <div
            v-for="position in defensePositions"
            :key="position"
            class="col text-center"
          >
            <div class="btn-group">
              <button
                :ref="'line' + index + position.abbr"
                type="button"
                class="btn btn-outline-primary dropdown-toggle"
                data-toggle="dropdown"
                aria-haspopup="true"
                aria-expanded="false"
              >
                {{ position.label }}
              </button>
              <div class="dropdown-menu">
                <span
                  @click="setPlayer(defenseman.name, index + position.abbr)"
                  v-for="defenseman in sortedDefense"
                  class="dropdown-item"
                  :key="defenseman.number"
                  >{{ defenseman.name }}
                  <span style="float:right" class="badge badge-dark">{{
                    defenseman.totalG
                  }}</span>
                  <span style="float:right" class="badge badge-danger">{{
                    defenseman.lastG
                  }}</span>
                  <span style="float:right" class="badge badge-primary">{{
                    defenseman.position
                  }}</span></span
                >
                <div class="dropdown-divider"></div>
                <span
                  @click="setPlayer(forward.name, index + position.abbr)"
                  v-for="forward in sortedForwards"
                  class="dropdown-item"
                  :key="forward.number"
                  >{{ forward.name }}
                  <span style="float:right" class="badge badge-dark">{{
                    forward.totalG
                  }}</span>
                  <span style="float:right" class="badge badge-danger">{{
                    forward.lastG
                  }}</span>
                  <span style="float:right" class="badge badge-primary">{{
                    forward.position
                  }}</span>
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
      <Goalies />
    </div>
    <div class="col-2">
      <h3 class="text-center">Roster</h3>
      <hr />
      <div
        v-for="player in sortedRoster"
        :key="player"
        class="custom-control custom-switch"
      >
        <input
          @click="setAttendance(player.id)"
          type="checkbox"
          class="custom-control-input"
          :id="'customSwitch' + player.number"
        />
        <label
          class="custom-control-label"
          :for="'customSwitch' + player.number"
          >{{ player.name }}</label
        >
      </div>
      <br />
      <Standings />
    </div>
  </div>
</template>

<script>
import Goalies from "./Goalies";
import json from "../json/relics.json";
import Standings from "./Standings.vue";
export default {
  name: "Skaters",
  components: {
    Goalies,
    Standings,
  },
  props: {
    team: String,
  },
  data() {
    return {
      defense: [],
      forwards: [],
      roster: json,
      defensePositions: [
        {
          abbr: "LD",
          label: "Left Defense",
        },
        {
          abbr: "RD",
          label: "Right Defense",
        },
      ],
      forwardPositions: [
        {
          abbr: "LW",
          label: "Left Winger",
        },
        {
          abbr: "C",
          label: "Center",
        },
        {
          abbr: "RW",
          label: "Right Winger",
        },
      ],
    };
  },
  methods: {
    compare(a, b) {
      if (a.name < b.name) return -1;
      if (a.name > b.name) return 1;
      return 0;
    },
    setAttendance(playerId) {
      this.roster[playerId].playing = !this.roster[playerId].playing;
    },
    setPlayer(playerName, positionRef) {
      // alert(this.$refs["line" + positionRef].innerText);
      this.$refs["line" + positionRef].innerText = playerName;
    },
  },
  computed: {
    sortedForwards() {
      return this.roster
        .filter((player) => {
          return (
            player.type.toLowerCase().includes("forward") && player.playing
          );
        })
        .sort(this.compare);
    },
    sortedDefense() {
      return this.roster
        .filter((player) => {
          return (
            player.type.toLowerCase().includes("defense") && player.playing
          );
        })
        .sort(this.compare);
    },
    sortedRoster() {
      return this.roster
        .filter(() => {
          return true;
        })
        .sort(this.compare);
    },
  },
  mounted() {
    //this.forwards = this.roster;
  },
};
</script>

<style scoped>
.badge-pill {
  text-align: right;
}
.blue {
  border: solid blue;
  /* display: inline-block; */
}
.dropdown-item {
  /* max-width: 100%; */
  width: 300px;
  /* white-space: nowrap; */
}
.faceoff {
  padding-block: 50px;
  text-align: center;
}
img {
  height: 200px;
  width: 200px;
  border-radius: 50%;
  border: 10px solid black;
}
#lines {
  padding-top: 10px;
}
.red {
  border: solid red;
  /* display: inline-block; */
}
.row,
.line {
  padding: 5px;
}
</style>
