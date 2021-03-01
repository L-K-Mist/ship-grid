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
            :stroke-width="maxX / 500"
          ></rect>
          <line
            v-for="x in maxX"
            :key="`vertical-${x}`"
            :x1="x"
            y1="0"
            :x2="x"
            :y2="maxY"
            stroke="black"
            :stroke-width="maxX / 1000"
          ></line>
          <line
            v-for="y in maxY"
            :key="`horizontal-${y}`"
            x1="0"
            :y1="y"
            :x2="maxX"
            :y2="y"
            stroke="blue"
            :stroke-width="maxX / 1000"
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
  width: 40vw;
}
.control-panel {
  position: absolute;
  bottom: 0px;
  width: 100%;
}
</style>
