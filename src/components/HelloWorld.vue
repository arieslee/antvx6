<template>
  <div>
    <div id="x6"></div>
    <!--    <button @click="add">外部 Add</button>-->
  </div>
</template>

<script>
import { Graph } from "@antv/x6";
import "@antv/x6-vue-shape";
import Count from "@/components/Count";
import { register } from "@antv/x6-vue-shape";
let graph = null;
export default {
  name: "App",
  mounted() {
    let w = window.outerHeight,
      h = window.outerHeight;
    graph = new Graph({
      container: document.getElementById("x6"),
      width: w,
      height: h,
      mousewheel: {
        enabled: true,
        modifiers: ["ctrl", "meta"],
        zoomAtMousePosition: false,
        global: true,
      },
      background: {
        position: "center",
        image: "./p1.jpeg",
      },
    });

    register({
      shape: "custom-vue-node",
      width: 100,
      height: 100,
      component: Count,
    });

    graph.addNode({
      id: "1",
      shape: "custom-vue-node",
      x: 200,
      y: 150,
      width: 150,
      height: 100,
      component: "count",
      data: {
        num: 0,
      },
    });
    graph.addNode({
      id: "2",
      shape: "custom-vue-node",
      x: 400,
      y: 150,
      width: 150,
      height: 100,
      data: {
        num: 0,
      },
    });
  },
  methods: {
    add() {
      const nodes = graph.getNodes();
      if (nodes.length) {
        nodes.forEach((node) => {
          const { num } = node.getData();
          node.setData({
            num: num + 1,
          });
        });
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
