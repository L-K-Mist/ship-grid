<template>
  <svg viewBox="0 0 50 50" id="ship-grid" width="50" height="50">
    <g id="group-grid" style="display: inline">
      <rect
        id="grid"
        :width="width"
        :height="height"
        fill="none"
        stroke="black"
        stroke-width="0.3"
      ></rect>
    </g>
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: Number,
      default: 10,
    },
    height: {
      type: Number,
      default: 10,
    },
  },
};
</script>

<style scoped></style>
