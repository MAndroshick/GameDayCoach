<template>
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
              <span class="badge badge-primary badge-pill">{{
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
              <span class="badge badge-primary badge-pill">{{
                defenseman.position
              }}</span></span
            >
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
              <span class="badge badge-primary badge-pill">{{
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
              <span class="badge badge-primary badge-pill">{{
                forward.position
              }}</span></span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import json from "../json/relics.json";
export default {
  name: "Skaters",
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
    setPlayer(playerName, positionRef) {
      // alert(this.$refs["line" + positionRef].innerText);
      this.$refs["line" + positionRef].innerText = playerName;
    },
  },
  computed: {
    sortedForwards() {
      function compare(a, b) {
        if (a.name < b.name) return -1;
        if (a.name > b.name) return 1;
        return 0;
      }
      return this.roster
        .filter((player) => {
          return player.type.toLowerCase().includes("forward");
        })
        .sort(compare);
    },
    sortedDefense() {
      function compare(a, b) {
        if (a.name < b.name) return -1;
        if (a.name > b.name) return 1;
        return 0;
      }
      return this.roster
        .filter((player) => {
          return player.type.toLowerCase().includes("defense");
        })
        .sort(compare);
    },
  },
  mounted() {
    this.forwards = this.roster;
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
