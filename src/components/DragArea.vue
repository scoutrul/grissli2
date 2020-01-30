<template>
  <div
    v-draggable
    @updatePosition="updatePosition"
    class="block"
    :style="
      `top: ${top}px; left: ${left}px; width: ${width}px; height: ${height}px; background: ${bgColor}`
    "
  >
    <div>position: {{ left }} x {{ top }}</div>
    <div>{{ name }}</div>
  </div>
</template>

<script>
export default {
  name: "DragArea",
  props: ["name", "changePosition", "bgColor"],
  data: () => ({ left: 0, top: 0, width: 200, height: 200 }),
  mounted() {
    const getRandomPosition = max => {
      max = max - this.width;
      return Math.floor(Math.random() * Math.floor(max));
    };

    let left = getRandomPosition(innerWidth);
    let top = getRandomPosition(innerHeight);
    this.updatePosition({ left, top });
  },
  methods: {
    updatePosition({ left, top }) {
      this.left = left;
      this.top = top;
      this.changePosition({ name: this.name, x: left, y: top });
    }
  },
  directives: {
    draggable: (el, binding, vNode) => {
      // console.log(binding, vNode);
      const updatePosition = vNode.data.on.updatePosition.fns;

      el.onmousedown = event => {
        el.style.zIndex = 1000;
        let shiftX = event.clientX - el.getBoundingClientRect().left;
        let shiftY = event.clientY - el.getBoundingClientRect().top;

        const onMouseMove = event => {
          let left = event.pageX - shiftX;
          let top = event.pageY - shiftY;
          // el.style.left = left;
          // el.style.top = top;
          updatePosition({ left, top });
        };

        document.addEventListener("mousemove", onMouseMove);

        el.onmouseup = () => {
          document.removeEventListener("mousemove", onMouseMove);
          el.onmouseup = null;
          el.style.zIndex = 1;
        };
      };
    }
  }
};
</script>

<style>
.block {
  position: absolute;
  z-index: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid #2c3e50;
}
</style>
