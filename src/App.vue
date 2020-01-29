<template>
  <div id="app">
    <DragArea name="first" :changePosition="changePosition" />
    <DragArea name="second" :changePosition="changePosition" />
    <DragArea name="third" :changePosition="changePosition" />
    <DragArea name="four" :changePosition="changePosition" />
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
  },
  data: () => ({
    items: {
      first: {
        x: 100,
        y: 100,
        bgColor: "grey",
        freeze: false,
        shrink: false
      }
    }
  }),
  methods: {
    changePosition({ name, x, y }) {
      this.items.first.x = x;
      this.items.first.y = y;
      // this.items[name].y = y;
      // ошибки

      // метод, который прокрутит все items
      // сравнит их позиции
      // если позиции близки к дропу (+- 50px)
      // то сравнить веса
      // если не фриз,
      // если ужато, когда внутри
      // то назначить им цвета
    }
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
  border: 1px solid #dd5533;
}
</style>
