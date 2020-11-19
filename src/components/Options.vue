<template>
  <div class="game-options">
    <h2>Game Options:</h2>
    <ul>
      <li v-for="(difficulty, index) in difficaltyLevels" :key="index">
        <input
          v-model="selectDifficulty"
          :value="difficulty.value"
          :id="`difficulty-${difficulty.value}`"
          type="radio"
          @change="changeInterval"
        />
        <label :for="`difficulty-${difficulty.value}`">{{
          difficulty.text
        }}</label>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: () => ({
    difficaltyLevels: {
      easy: {
        value: "easy",
        text: "Easy",
        interval: 1500,
      },
      medium: {
        value: "medium",
        text: "Medium",
        interval: 1000,
      },
      hard: {
        value: "hard",
        text: "Hard",
        interval: 400,
      },
    },
    selectDifficulty: "easy",
  }),
  computed: {
    interval() {
      return this.difficaltyLevels[this.selectDifficulty].interval;
    },
  },
  methods: {
    changeInterval() {
      this.$emit("changeinterval", this.interval);
    },
  },
};
</script>

<style>
</style>