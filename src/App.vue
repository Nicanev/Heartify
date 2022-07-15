<script setup>
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";
import Sidebar from "./components/SideBar.vue";
import Player from "./components/Player.vue";
</script>

<template>
  <div class="wrapper">
    <Header class="header" />
    <Sidebar class="sidebar" @pos="resizeSideBar" :style="{ width: resizeX }" />
    <Content class="content" />
    <Player class="player" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      menuPositionX: "",
      menuPositionY: "",
      resizeX: "250px",
    };
  },
  methods: {
    resizeSideBar(e) {
      let position = this.getPosition(e);
      this.resizeX = position.x + "px";
    },
    getPosition(e) {
      let posx;
      let posy;
      posx = e.pageX;
      posy = e.pageY;

      return {
        x: posx,
        y: posy,
      };
    },
  },
};
</script>

<style lang="scss">
.wrapper {
  display: grid;
  min-height: 100vh;
  grid-template-columns: auto 1fr 1fr;
  grid-template-areas: "sd hd hd" "sd main main" "pl pl pl";
  grid-template-rows: auto 1fr auto;
  color: white;
}
.sidebar {
  grid-area: sd;
  background: #111216;
  max-width: 400px;
  min-width: 200px;
}
.header {
  grid-area: hd;
  height: 50px;
  position: relative;
  z-index: 2;
}
.player {
  grid-area: pl;
  height: 90px;
}
.content {
  grid-area: main;
  position: relative;
  z-index: 1;
  overflow: auto;
  max-height: 810px;
  grid-row: 1 / 3;
}
</style>
