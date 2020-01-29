<template>
  <div
    v-draggable
    @updatePosition="updatePosition"
    class="block"
    :style="`top: ${top}; left: ${left}`"
  >
    <div>position: {{ left }} x {{ top }}</div>
    <div>{{ name }}</div>
  </div>
</template>

<script>
export default {
  name: "DragArea",
  props: ["name"],
  data: () => ({ left: 0, top: 0 }),
  mounted() {
    const getRandomPosition = max => {
      max = max - 200;
      return Math.floor(Math.random() * Math.floor(max));
    };

    let left = getRandomPosition(innerWidth) + "px";
    let top = getRandomPosition(innerHeight) + "px";
    this.updatePosition(left, top);
  },
  methods: {
    updatePosition(left, top) {
      const $left = left;
      const $top = top;
      if (left !== $left && top !== $top) {
        // debugger;
      }
      this.left = left;
      this.top = top;
    }
  },
  directives: {
    draggable: (el, binding, vNode) => {
      // const updatePosition = vNode.data.on.updatePosition.fns;
      const updatePosition = vNode.context.$emit('updatePosition');
      

      el.onmousedown = event => {
        el.style.zIndex = 1000;
        let shiftX = event.clientX - el.getBoundingClientRect().left;
        let shiftY = event.clientY - el.getBoundingClientRect().top;

        const onMouseMove = event => {
          let left = event.pageX - shiftX + "px";
          let top = event.pageY - shiftY + "px";
          // el.style.left = left;
          // el.style.top = top;
          updatePosition(left, top);
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
  height: 200px;
  width: 200px;
  border: 1px solid #2c3e50;
}
</style>
