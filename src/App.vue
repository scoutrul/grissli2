<template>
  <div id="app">
    <DragArea name="first"/>
    <DragArea name="second"/>
    <DragArea name="third"/>
    <DragArea name="four"/>
    <div class="droppable">
      <div>
        drop area
      </div>
    </div>
  </div>
</template>

<script>
import DragArea from "./components/DragArea.vue";

export default {
  name: "app",
  components: {
    DragArea
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
  .droppable {
    position: absolute;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 200px;
    width: 200px;
    border: 1px solid #DD5533;
  }
</style>
