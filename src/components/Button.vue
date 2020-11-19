<template>
  <button class="tile" :class="buttonColor" @click="handleClick" ref="button" />
</template>

<script>
export default {
  props: {
    index: Number,
    color: String,
    name: String,
  },
  data: () => ({
    sound: null,
  }),

  created() {
    const path = require(`@/assets/sounds/${this.name}`);
    this.sound = new Audio(path);
  },

  computed: {
    buttonColor() {
      return this.color;
    },
  },

  methods: {
    animateButton() {
      this.sound.play();

      this.$refs.button.classList.add("active");
      setTimeout(() => {
        this.$refs.button.classList.remove("active");
      }, 400);
    },

    handleClick() {
      this.animateButton();
      this.$emit("click", this.index);
    },
  },
};
</script>

<style>
</style>