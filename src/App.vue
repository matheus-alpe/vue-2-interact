<template>
  <WhiteBoard>
    <DraggableText msg="teste 1" id="1"/>
    <DraggableText msg="palavra 2" id="2"/>
  </WhiteBoard>
</template>

<script>
import WhiteBoard from './components/WhiteBoard.vue'
import DraggableText from './components/DraggableText.vue'

export default {
  name: 'App',
  components: {
    DraggableText,
    WhiteBoard
  }
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
