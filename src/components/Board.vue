<template>
  <div class="game-board">
    <div class="simon">
      <ul class="simon-template">
        <li v-for="(button, index) in buttons" :key="index">
          <Button
            ref="button"
            :index="index"
            :color="button.color"
            :name="button.name"
            @click="handleClick"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue";

export default {
  components: {
    Button,
  },
  data: () => ({
    buttons: [
      {
        color: "blue",
        name: "1.mp3",
      },
      {
        color: "red",
        name: "2.mp3",
      },
      {
        color: "yellow",
        name: "3.mp3",
      },
      {
        color: "green",
        name: "4.mp3",
        sound: null,
      },
    ],
    sound: null,
  }),

  methods: {
    handleClick(idx) {
      this.$emit("click", idx);
    },
  },
};
</script>

<style>
</style>