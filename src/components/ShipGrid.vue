<template>
  <div>
    <v-row class="svg-wrapper">
      <svg viewBox="0 0 50 50" id="ship-grid" width="50" height="50">
        <g id="group-grid" style="display: inline">
          <rect
            id="grid"
            :width="maxX"
            :height="maxY"
            fill="none"
            stroke="black"
            stroke-width="0.3"
          ></rect>
          <line
            v-for="item in maxX"
            :key="item"
            :x1="item"
            y1="0"
            :x2="item"
            :y2="maxY"
            stroke="black"
            stroke-width="0.1"
          ></line>
          <line
            v-for="item in maxY"
            :key="item"
            x1="0"
            :y1="item"
            :x2="maxX"
            :y2="item"
            stroke="blue"
            stroke-width="0.1"
          ></line>
        </g>
      </svg>
    </v-row>
    <v-row class="control-panel pa-2">
      <v-slider
        lazy
        thumb-label="always"
        label="Max X"
        v-model="maxX"
        max="50"
      ></v-slider>
      <v-slider
        lazy
        thumb-label="always"
        label="Max Y"
        v-model="maxY"
        max="50"
      ></v-slider>
      <v-btn @click="zoomToView('grid')" color="primary">Center the Grid</v-btn>
    </v-row>
  </div>
</template>

<script>
import { gsap } from "gsap";
export default {
  data() {
    return {
      maxX: 10,
      maxY: 12,
    };
  },

  methods: {
    viewBoxString(frame) {
      return `${frame.x - 1} ${frame.y + 1} ${frame.width + 2} ${frame.height -
        2}`;
    },
    zoomToView(elementId) {
      const element = document.getElementById(elementId);
      const box = element.getBBox();
      return gsap.to("#ship-grid", {
        duration: 1,
        attr: { viewBox: this.viewBoxString(box) },
      });
    },
  },
};
</script>

<style scoped>
svg {
  border: 2px dotted blue;
  margin: 20px 0;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}
.svg-wrapper {
  margin: 40px auto;
  height: 60vh;
  width: 60vw;
}
.control-panel {
  position: absolute;
  bottom: 0px;
  width: 100%;
}
</style>
