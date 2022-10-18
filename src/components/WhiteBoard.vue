<template>
  <div ref="board">
    <div
      class="board"
      :style="style"
      @dblclick.stop="addItem"
    >
      <img :src="bgImage || require('@/assets/background.jpg')" alt="bg" :style="imgStyle" />
      <slot />
    </div>
  </div>
</template>

<script>
import { VIEW_SIZE } from '@/utils'

export default {
  name: 'WhiteBoard',

  props: {
    view: {
      type: String,
      required: true,
      validator: (view) => Object.keys(VIEW_SIZE).includes(view),
    },

    bgImage: {
      type: String,
      default: () => require('@/assets/background.jpg')
    }
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
        'user-drag': 'none',
        'cursor': 'text'
      },
    }
  },

  methods: {

    /**
     * 
     * @param {MouseEvent} event 
     */
    addItem(event) {
      if (this.view !== 'full' || event.target.nodeName !== 'IMG') return


      this.$emit('addItem', {
        x: (event.layerX - VIEW_SIZE[this.view]) / VIEW_SIZE[this.view],
        y: (event.layerY - VIEW_SIZE[this.view]) / VIEW_SIZE[this.view],
      })
    },
  },
}
</script>
