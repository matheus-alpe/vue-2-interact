<template>
  <p
    :ref="item.id"
    :class="item.id"
    :contenteditable="!isPreview"
    :style="style"
    @blur="editHandler"
    @dblclick.stop.capture="deleteHandler"
    v-html="item.message"
  >
  </p>
</template>

<script>
import interact from 'interactjs'
import { VIEW_SIZE } from '@/utils'

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

    viewEmSize: {
      type: Number,
      default: () => VIEW_SIZE.full
    }
  },

  data() {
    return {
      position: { x: 0, y: 0 },

      style: {
        margin: 0,
        padding: 0,
        'font-size': '1em',
        color: '#000',
        width: 'fit-content',
        position: 'absolute',
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

    editHandler (event) {
      if (this.isPreview) return
      
      const content = event.target.innerHTML.trim()
      if (!content) return this.deleteHandler()
      this.$emit('edited', content)
    },

    deleteHandler () {
      if (this.isPreview) return
      this.$emit('deleted', this.item.id)
    },
  },

  created() {
    this.position = { ...this.item.position }
  },

  mounted() {
    this.moveElement(this.$refs[this.item.id], this.position)
    if (this.isPreview) return

    if (!this.item.message) this.$refs[this.item.id].focus()


    interact(`.${this.item.id}`).draggable({
      listeners: {
        move: (event) => {
          this.position.x += event.dx / this.viewEmSize
          this.position.y += event.dy / this.viewEmSize

          this.moveElement(event.target, this.position)
        },

        end: () => {
          this.$emit('moveEnd', this.position)
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
