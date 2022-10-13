<template>
  <WhiteBoard>
    <DraggableText msg="teste 1" id="1"/>
    <DraggableText msg="Insira algum texto" id="2"/>
    <DraggableText :msg="'Hash de validação: {{ hash }}'" id="3"/>
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
