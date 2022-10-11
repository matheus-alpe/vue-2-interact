<template>
  <p :class="`text-label-${id}`" contenteditable="true" :style="style">
    {{ msg }}
  </p>
</template>

<script>
import interact from "interactjs";

export default {
  name: "DraggableText",

  props: {
    msg: String,

    id: {
      type: String,
      required: true,
    },
  },

  data() {
    return {
      position: { x: 0, y: 0 },

      style: {
        margin: 0,
        "font-size": "1em",
        padding: "5px",
        color: "#000",
        "max-width": "fit-content",
        position: "absolute",
      },
    };
  },

  mounted() {
    interact(`.text-label-${this.id}`)
      .draggable({
        listeners: {
          move: (event) => {
            this.position.x += event.dx;
            this.position.y += event.dy;

            event.target.style.transform = `translate(${this.position.x}px, ${this.position.y}px)`;
          },
        },
      })
  },
};
</script>