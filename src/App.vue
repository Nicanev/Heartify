<script setup>
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";
import Sidebar from "./components/SideBar.vue";
import Player from "./components/Player.vue";
</script>

<template>
  <div class="wrapper">
    <Header
      class="header"
      :style="{ background: 'rgba(27, 54, 43,' + opacity + '%' + ')' }"
    />
    <Sidebar class="sidebar" @pos="resizeSideBar" :style="{ width: resizeX }" />
    <Content class="content" @scroll="onScroll" />
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
      opacity: 0,
    };
  },
  methods: {
    resizeSideBar(e) {
      let position = this.getPosition(e);
      this.resizeX = position.x + "px";
    },
    onScroll() {
      let main = document.getElementById("main");
      let scroll = main.scrollTop;

      if (scroll > 225 || scroll < 235) {
        this.opacity = 10;
      }
      if (scroll > 235 || scroll < 245) {
        this.opacity = 20;
      }
      if (scroll > 245 || scroll < 255) {
        this.opacity = 30;
      }
      if (scroll > 255 || scroll < 265) {
        this.opacity = 40;
      }
      if (scroll > 265 || scroll < 275) {
        this.opacity = 50;
      }
      if (scroll > 275) {
        this.opacity = 100;
      }
      if (scroll < 225) {
        this.opacity = 0;
      }
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

<style lang="scss" scoped>
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
  height: 70px;
  position: relative;
  background: rgba(27, 54, 43, 100%);
  transition: 0.2s;
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
