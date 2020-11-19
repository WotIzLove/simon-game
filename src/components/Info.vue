<template>
  <div class="game-info">
    <h2>
      Round: <span data-round="0">{{ round }}</span>
    </h2>
    <button @click="init">Start</button>
    <p v-if="gameover">Sorry, you lost after {{ round }} rounds!</p>
  </div>
</template>

<script>
export default {
  props: {
    current: Number,
    gameover: Boolean,
    round: Number,
  },
  methods: {
    init() {
      this.$emit("init");
    },
  },
};
</script>

<style>
</style>