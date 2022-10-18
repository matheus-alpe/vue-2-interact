<template>
  <div style="position: relative; min-height: 100vh; padding: 0; margin: 0">
    <div>
      <p>Text Instructions:</p>
      <ol>
        <li>ADD: Click two times over background image</li>
        <li>EDIT: Click one time over a text</li>
        <li>DELETE: Click two times over a text</li>
      </ol>
    </div>
    <div>
      <label for="image">Change background: </label>
      <input
        @change="previewFiles"
        type="file"
        name="image"
        id="image"
        accept="image/*"
      />
    </div>
    <WhiteBoard view="full" @addItem="addItem" :bgImage="imgInput">
      <DraggableText
        v-for="item in items"
        :item="item"
        :key="item.id"
        @moveEnd="(newPosition) => updateItem(item, 'position', newPosition)"
        @edited="(newMessage) => updateItem(item, 'message', newMessage)"
        @deleted="removeItem"
      />
    </WhiteBoard>

    <WhiteBoard view="preview" style="position: absolute; right: 0; bottom: 0; border: 1px solid red;" :bgImage="imgInput">
      <DraggableText
        v-for="item in items"
        :item="{ ...item, id: `preview-${item.id}` }"
        :key="`preview-${item.id}`"
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
      imgInput: null,
      items: [
        {
          id: randomId(),
          message:
            'Teste asdas<div><br></div><div>&nbsp; &nbsp; asdsad</div><div>1asdasd</div>',
          position: {
            x: 27.599999999999973,
            y: 12.600000000000025,
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
    addItem(position) {
      this.items.push({
        id: randomId(),
        message: 'Insira algum texto',
        position,
      })
    },

    removeItem(itemId) {
      this.items = this.items.filter((item) => item.id !== itemId)
    },

    updateItem(item, key, value) {
      if (!item.id) return
      item[key] = value
    },

    previewFiles(event) {
        const [ file ] = event.target.files
        if (!file) return

        var reader = new FileReader();

        reader.onload = (event) => {
          this.imgInput = event.target.result;
        };

        reader.readAsDataURL(file);
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
