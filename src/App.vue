<template>
  <v-app :style="{ background: 'hsl(202deg 99% 95%)' }">
    <text-based-solution></text-based-solution>
    <v-btn
      @click="showShipGrid = true"
      id="ship-grid-button"
      color="hsl(44deg 95% 50%)"
      >Try out the early-stage ship-grid</v-btn
    >
    <v-dialog
      v-model="showShipGrid"
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
    >
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="showShipGrid = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>Ship Grid</v-toolbar-title>
        </v-toolbar>
        <div class="ship-grid-wrapper">
          <ship-grid></ship-grid>
        </div>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import TextBasedSolution from "@/components/TextBasedSolution";
import ShipGrid from "@/components/ShipGrid";
export default {
  name: "App",
  components: {
    TextBasedSolution,
    ShipGrid,
  },
  data() {
    return {
      showShipGrid: true,
    };
  },
};
</script>

<style scoped>
#ship-grid-button {
  position: absolute;
  right: 30px;
  bottom: 30px;
}
.ship-grid-wrapper {
  height: 70vh;
}
</style>
