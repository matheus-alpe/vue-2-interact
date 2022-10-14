<template>
  <p :ref="item.id" :class="item.id" :contenteditable="!isPreview" :style="style" @blur="handleBlur" v-html="item.message">
  </p>
</template>

<script>
import interact from 'interactjs'

export default {
  name: 'DraggableText',

  props: {
    item: {
      type: Object,
      default: () => {},
    },

    isPreview: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      position: { x: 0, y: 0 },

      style: {
        margin: 0,
        'font-size': '1em',
        padding: '5px',
        color: '#000',
        width: 'fit-content',
        position: 'absolute',
        'user-select': 'none',
      },
    }
  },

  watch: {
    'item.position': {
      deep: true,
      handler() {
        if (!this.isPreview) return
        this.moveElement(this.$refs[this.item.id], this.item.position)
      },
    },
  },

  methods: {
    moveElement(element, position) {
      Object.assign(element.style, {
        transform: `translate(${position.x}em, ${position.y}em)`,
      })
    },

    handleBlur(e) {
      if (!this.isPreview) return
      this.$emit('edited', this.item.id, e.target.innerHTML.trim())
    }
  },

  created() {
    this.position = { ...this.item.position }
  },

  mounted() {
    this.moveElement(this.$refs[this.item.id], this.position)
    if (this.isPreview) return

    interact(`.${this.item.id}`).draggable({
      listeners: {
        move: (event) => {
          this.position.x += event.dx / 75
          this.position.y += event.dy / 75

          this.moveElement(event.target, this.position)
        },

        end: () => {
          this.$emit('moveEnd', this.item.id, this.position)
        },
      },
    })

    // .resizable({
    //   edges: { top: false, left: false, bottom: false, right: true },
    //   listeners: {
    //     move: (event) => {
    //       Object.assign(event.target.style, {
    //         width: `${event.rect.width}px`,
    //       });
    //     },
    //   },
    // });
  },
}
</script>
