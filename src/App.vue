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
    <Content
      class="content"
      @scroll="onScroll"
      @track="getTrack"
      @context-menu="getContextMenuStatus"
      @click.right="openContextMenu"
      :switch="switch"
      :playStatus="playStatus"
    />
    <Player
      class="player"
      :track="track"
      @switch="getSwitch"
      @playStatus="getPlayStatus"
    />
    <div
      class="context-menu"
      :style="{ left: menuPositionX, top: menuPositionY }"
      v-if="isContextMenyActive"
    >
      <ul>
        <li><a href="#">Play</a></li>
        <li><a href="#">Add to queue</a></li>
        <li><a href="#">Add to playlist</a></li>
      </ul>
    </div>
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
      track: null,
      switch: null,
      playStatus: null,
      isContextMenyActive: false,
    };
  },
  created() {
    document.addEventListener(
      "click",
      () => (this.isContextMenyActive = false)
    );
  },
  methods: {
    getContextMenuStatus(status) {
      if (status == true) {
        this.isContextMenyActive = true;
      } else {
        this.isContextMenyActive = false;
      }
    },
    resizeSideBar(e) {
      let position = this.getPosition(e);
      this.resizeX = position.x + "px";
    },
    getTrack(track) {
      this.track = track;
    },
    getSwitch(switchStatus) {
      this.switch = switchStatus;
    },
    getPlayStatus(playStatus) {
      this.playStatus = playStatus;
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
    openContextMenu(e) {
      e.preventDefault();

      let menuPosition = this.getPosition(e);
      this.menuPositionX = menuPosition.x + "px";
      this.menuPositionY = menuPosition.y + "px";
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
.context-menu {
  position: absolute;
  z-index: 1000;
  background-color: rgb(27, 27, 27);
  width: max-content;
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  li {
    padding: 15px;
    cursor: pointer;
  }
  li:hover {
    background-color: rgba(66, 66, 66, 0.562);
  }
  a {
    color: white;
  }
}
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
  @media screen and (min-height: 950px) {
    max-height: 870px;
  }
}
</style>
