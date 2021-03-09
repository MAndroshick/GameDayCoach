<template>
  <div>
    <h3 class="text-center">Standings</h3>
    <hr />
    <div v-for="team in sortedStandings" :key="team">
      <span class="badge badge-dark">{{ team.rank }}</span>
      {{ team.team }}
    </div>
  </div>
</template>

<script>
import json from "../json/standings.json";
export default {
  name: "Standings",
  data() {
    return {
      standings: json,
    };
  },
  methods: {
    compareRank(a, b) {
      if (a.rank < b.rank) return -1;
      if (a.rank > b.rank) return 1;
      return 0;
    },
  },
  computed: {
    sortedStandings() {
      return this.standings
        .filter(() => {
          return true;
        })
        .sort(this.compareRank);
    },
  },
};
</script>

<style></style>
