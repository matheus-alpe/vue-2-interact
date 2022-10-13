<template>
  <div ref="board">
    <div class="board" :style="style" @click="handleClick">
      <img src="@/assets/background.jpg" alt="bg" :style="imgStyle" />
      <slot />
    </div>
  </div>
</template>

<script>
// const BOARD_WIDTH = "3508px"
// const BOARD_HEIGHT = "2450px"

export default {
  name: "WhiteBoard",

  data() {
    return {
      style: {
        "font-size": "76px",
        background: "#fff",
        width: "46.1578947368421em",
        "max-width": "46.1578947368421em",
        height: "32.23684210526316em",
        "max-height": "32.23684210526316em",
        overflow: "hidden",
        position: "relative",
      },

      imgStyle: {
        width: "46.1578947368421em",
        "max-width": "46.1578947368421em",
        height: "32.23684210526316em",
        "max-height": "32.23684210526316em",
        display: "block",
        position: 'absolute',
        top: 0,
        left: 0
      },
    };
  },

  methods: {
    handleClick() {
      if (!this.$refs.board) return;
      console.log(this.$refs.board.innerHTML);
    },
  },
};
</script>