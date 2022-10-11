<template>
  <div ref="board">
    <div class="board" :style="style" @click="handleClick">
      <img src="@/assets/background.jpg" alt="bg" :style="imgStyle" />
      <slot />
    </div>
  </div>
</template>

<script>
const BOARD_WIDTH = "1408px"
// const BOARD_WIDTH = "3508px"
const BOARD_HEIGHT = "950px"
// const BOARD_HEIGHT = "2450px"

export default {
  name: "WhiteBoard",

  data() {
    return {
      style: {
        "font-size": "76px",
        background: "#fff",
        width: BOARD_WIDTH,
        "max-width": BOARD_WIDTH,
        height: BOARD_HEIGHT,
        "max-height": BOARD_HEIGHT,
        overflow: "hidden",
        position: "relative",
      },

      imgStyle: {
        width: BOARD_WIDTH,
        "max-width": BOARD_WIDTH,
        height: BOARD_HEIGHT,
        "max-height": BOARD_HEIGHT,
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