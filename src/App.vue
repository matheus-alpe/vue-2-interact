<template>
  <div style="position: relative; min-height: 100vh; padding: 0; margin: 0">
    <WhiteBoard view="full" @addElement="addElement">
      <DraggableText
        v-for="item in items"
        :item="item"
        :key="item.id"
        @moveEnd="updatePositionState"
      />
    </WhiteBoard>

    <WhiteBoard view="preview" style="position: absolute; left: 0; bottom: 0">
      <DraggableText
        v-for="item in items"
        :item="{ ...item, id: `preview-${item.id}` }"
        :key="`preview-${item.id}`"
        :is-preview="true"
      />
    </WhiteBoard>

    <WhiteBoard
      view="small-preview"
      style="position: absolute; right: 0; bottom: 0"
    >
      <DraggableText
        v-for="item in items"
        :item="{ ...item, id: `small-preview-${item.id}` }"
        :key="`small-preview-${item.id}`"
        :is-preview="true"
      />
    </WhiteBoard>
  </div>
</template>

<script>
import { randomId } from '@/utils'

import WhiteBoard from './components/WhiteBoard.vue'
import DraggableText from './components/DraggableText.vue'

export default {
  name: 'App',
  components: {
    DraggableText,
    WhiteBoard,
  },

  data() {
    return {
      items: [
        {
          id: randomId(),
          message: 'Teste 1',
          position: {
            x: 20,
            y: 20,
          },
        },
        {
          id: randomId(),
          message: 'Hash de validação: {{ hash }}',
          position: {
            x: 8.040000000000102,
            y: 8.40000000000002,
          },
        },
      ],
    }
  },

  methods: {
    addElement(position) {
      this.items.push({
        id: randomId(),
        message: 'Insira algum texto',
        position,
      })
    },

    updatePositionState(itemId, newPosition) {
      console.log('updatePositionState', itemId, newPosition)

      this.items.forEach((item) => {
        if (item.id === itemId) {
          item.position = {
            ...newPosition,
          }
        }
      })
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
</style>
