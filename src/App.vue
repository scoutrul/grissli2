<template>
  <div id="app">
    <DragArea
      v-for="(item, i) in items"
      :key="i"
      :name="item.name"
      :changePosition="changePosition"
      :bgColor="item.bgColor"
    />
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
        name: "first",
        bgColor: "grey",
        freeze: false,
        shrink: false
      },
      second: {
        name: "second"
      },
      third: {
        name: "third"
      },
      four: {
        name: "four"
      }
    }
  }),
  methods: {
    changePosition({ name, x, y }) {
      this.items = {
        ...this.items,
        [name]: {
          ...this.items[name],
          x,
          y
        }
      };
      // this.checkItem({ name, x, y });
      this.checkDropZone({ name, x, y });

      // метод, который прокрутит все items
      // сравнит их позиции
      // если позиции близки к дропу (+- 50px)
      // то сравнить веса
      // если не фриз,
      // если ужато, когда внутри
      // то назначить им цвета
    },
    checkItem({ name, x, y }) {
      // debugger;
      let elem = document.elementFromPoint(x, y);

      elem.style.background = "pink";
    },
    checkDropZone({ name, x, y }) {
      let dropZone = document
        .getElementsByClassName("droppable")[0]
        .getBoundingClientRect();
      let condition = x > dropZone.x - 100 && y > dropZone.y - 100;
      if (condition) {
        this.items[name].bgColor = "black";
      } else {
        this.items[name].bgColor = "pink";
      }
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
