<template>
  <div ref="board">
    <div
      class="board"
      :style="style"
      @click="handleClick"
      @dblclick="handleDoubleClick"
    >
      <img src="@/assets/background.jpg" alt="bg" :style="imgStyle" />
      <slot />
    </div>
  </div>
</template>

<script>
const VIEW_SIZE = {
  full: 76,
  preview: 32,
  'small-preview': 11,
}

export default {
  name: 'WhiteBoard',

  props: {
    view: {
      type: String,
      required: true,
      validator: (view) => Object.keys(VIEW_SIZE).includes(view),
    },
  },

  data() {
    return {
      style: {
        'font-size': VIEW_SIZE[this.view] + 'px',
        background: '#fff',
        width: '46.1578947368421em',
        'max-width': '46.1578947368421em',
        height: '32.23684210526316em',
        'max-height': '32.23684210526316em',
        overflow: 'hidden',
        position: 'relative',
      },

      imgStyle: {
        width: '46.1578947368421em',
        'max-width': '46.1578947368421em',
        height: '32.23684210526316em',
        'max-height': '32.23684210526316em',
        display: 'block',
        position: 'absolute',
        top: 0,
        left: 0,
        'user-select': 'none',
      },
    }
  },

  methods: {
    handleClick() {
      // console.log(this.$refs.board.innerHTML);
    },

    handleDoubleClick(event) {
      if (event.target.nodeName === 'IMG') {
        return this.$emit('addElement', {
          x: event.x / VIEW_SIZE[this.view],
          y: event.y / VIEW_SIZE[this.view],
        })
      }

      this.deleteElement(event.target)
    },

    /**
     *
     * @param {HTMLElement} element
     */
    deleteElement(element) {
      if (!element) return
      element.remove()
    },
  },
}
</script>
