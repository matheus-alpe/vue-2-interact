<template>
  <p class="text-label" contenteditable="true" :style="style">
    {{ msg }}
  </p>
</template>

<script>
import interact from "interactjs";

export default {
  name: "TextLabel",

  props: {
    msg: String,
  },

  data() {
    return {
      position: { x: 0, y: 0 },

      style: {
        margin: 0,
        padding: '5px',
        color: '#000',
        'max-width': 'fit-content'
      }
    }
  },

  mounted() {
    interact(".text-label").draggable({
      listeners: {
        start: (event) => {
          console.log(event.type, event.target);
        },
        move: (event) => {
          this.position.x += event.dx;
          this.position.y += event.dy;

          event.target.style.transform = `translate(${this.position.x}px, ${this.position.y}px)`;
        },
      },
    });
  },
};
</script>