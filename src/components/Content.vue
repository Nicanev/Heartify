<template>
  <div class="main" id="main">
    <div class="main__background"></div>
    <div class="main__content">
      <div class="playlist">
        <div class="playlist__header">
          <div class="playlist__image">
            <img src="../static/img/playlist-img.png" alt="playlist image" />
          </div>
          <div class="playlist__text">
            <div class="playlist__title">Liked songs</div>
            <div class="playlist__info">
              <span>Playlist</span><span class="sep"></span>
              <span>4 songs</span>
            </div>
          </div>
        </div>
        <div class="playlist__main">
          <div class="playlist__control-panel">
            <div class="circle-big">
              <img src="../static/img/icons/Play.svg" alt="" />
            </div>
          </div>
          <div class="playlist__table">
            <table cellspacing="0">
              <tr>
                <th align="center">#</th>
                <th align="left"><span>TITLE</span></th>
                <th align="left"><span>ALBUM</span></th>
                <th align="left"><span>DATE ADDED</span></th>
                <th align="left">
                  <svg
                    width="28"
                    height="28"
                    viewBox="0 0 28 28"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      fill-rule="evenodd"
                      clip-rule="evenodd"
                      d="M23 14C23 18.9706 18.9706 23 14 23C9.02944 23 5 18.9706 5 14C5 9.02944 9.02944 5 14 5C18.9706 5 23 9.02944 23 14ZM25 14C25 20.0751 20.0751 25 14 25C7.92487 25 3 20.0751 3 14C3 7.92487 7.92487 3 14 3C20.0751 3 25 7.92487 25 14ZM14.5 8.5H12.5V15.5H18V13.5H14.5V8.5Z"
                      fill="#9C9C9D"
                    />
                  </svg>
                </th>
              </tr>
              <tr class="separator" />
              <tr
                v-for="(song, index) in songs"
                v-bind:key="song"
                @mouseover="mouseOverSong(index)"
                @mouseleave="mouseLeaveSong"
                @click="selectItem($event, index)"
                @click.right="openContextMenu"
                :class="{
                  playing: playingID == index,
                  'selected-item': song.isSelect,
                }"
              >
                <td
                  class="id"
                  v-if="mouseOver != index && (!isPlay || playingID != index)"
                  align="center"
                >
                  {{ index + 1 }}
                </td>
                <td
                  v-if="mouseOver != index && isPlay && playingID == index"
                  align="center"
                >
                  <svg
                    width="28"
                    height="28"
                    viewBox="0 0 28 28"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <rect x="6" y="5" width="3" height="18" fill="#65D36E" />
                    <rect x="10" y="19" width="3" height="4" fill="#65D36E" />
                    <rect x="14" y="9" width="3" height="14" fill="#65D36E" />
                    <rect x="18" y="19" width="3" height="4" fill="#65D36E" />
                  </svg>
                </td>
                <td class="play-btn" v-if="mouseOver == index" align="center">
                  <svg
                    v-if="!isPlay || playingID != index"
                    @click="play(song, index)"
                    width="13"
                    height="14"
                    viewBox="0 0 13 14"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      d="M1.50171 14C1.25225 13.9996 1.0072 13.9383 0.790673 13.8223C0.303105 13.5636 0 13.0615 0 12.5163V1.48376C0 0.937074 0.303105 0.436424 0.790673 0.177729C1.01235 0.0584393 1.26419 -0.00290576 1.51985 0.000105775C1.77552 0.00311731 2.02562 0.0703751 2.24403 0.194849L12.3143 5.83895C12.5242 5.96217 12.6972 6.13328 12.8172 6.33623C12.9371 6.53918 13 6.76733 13 6.99927C13 7.23122 12.9371 7.45936 12.8172 7.66232C12.6972 7.86527 12.5242 8.03638 12.3143 8.15959L2.24241 13.8052C2.0189 13.9317 1.76289 13.9991 1.50171 14V14Z"
                      fill="white"
                    />
                  </svg>
                  <svg
                    v-if="isPlay && playingID == index"
                    @click="play(song, index)"
                    width="13"
                    height="14"
                    viewBox="0 0 13 14"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      d="M4.5194 12.05C4.5194 13.1269 3.50763 14 2.2597 14C1.01177 14 0 13.1269 0 12.05V1.95001C0 0.873107 1.01177 0 2.2597 0C3.50763 0 4.5194 0.873107 4.5194 1.95001V12.05Z"
                      fill="white"
                    />
                    <path
                      d="M13 12.05C13 13.1269 11.9882 14 10.7403 14C9.49236 14 8.48059 13.1269 8.48059 12.05V1.95001C8.48093 0.873107 9.4927 0 10.7403 0C11.9882 0 13 0.873107 13 1.95001V12.05Z"
                      fill="white"
                    />
                  </svg>
                </td>
                <td valign="middle">
                  <div class="playlist__track-info track-info">
                    <div class="track-info__img">
                      <img
                        :src="'/src/static/img/albums/' + song.album_img"
                        alt=""
                      />
                    </div>
                    <div class="track-info__text">
                      <div class="track-info__title">
                        <a href="#">{{ song.title }}</a>
                      </div>
                      <div class="track-info__performer">
                        <a href="#">{{ song.perform }}</a>
                      </div>
                    </div>
                  </div>
                </td>
                <td class="album">
                  <a href="#">{{ song.album }}</a>
                </td>
                <td class="date-add">{{ song.date_ad }}</td>
                <td class="duration">{{ getTime(song.duration) }}</td>
              </tr>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["switch", "playStatus"],
  data() {
    return {
      songs: [
        {
          title: "Relight",
          perform: "DSTechnician",
          album: "DSTechnicianl",
          album_img: "unknown.jpg",
          src: "relight.mp3",
          date_ad: "4 hours ago",
          duration: 66,
          isSelect: false,
        },
        {
          title: "Relics",
          perform: "DSTechnician",
          album: "DSTechnicianl",
          album_img: "unknown.jpg",
          src: "relics.mp3",
          date_ad: "4 hours ago",
          duration: 347,
          isSelect: false,
        },
        {
          title: "Let The Games Begin",
          perform: "Psychronic",
          album: "Psychronic",
          album_img: "unknown.jpg",
          src: "let-the-games-begin.mp3",
          date_ad: "4 hours ago",
          duration: 162,
          isSelect: false,
        },
        {
          title: "Pixel Perfect",
          perform: "DeepMusicEveryDay",
          album: "DeepMusicEveryDay",
          album_img: "unknown.jpg",
          src: "pixel-perfect.mp3",
          date_ad: "4 hours ago",
          duration: 91,
          isSelect: false,
        },
      ],
      mouseOver: null,
      formatTimeEnd: "",
      playingID: null,
      isPlay: null,
      isContextMenuActive: false,
    };
  },
  mounted() {
    this.$emit("track", this.songs[0]);
    window.addEventListener("keydown", (e) => {
      this.isContextMenuActive = false;
      this.$emit("context-menu", this.isContextMenuActive);
      if (e.key == "Escape") {
        this.songs.forEach(function (item) {
          if (item.isSelect == true) {
            item.isSelect = false;
          }
        });
      }
    });
  },
  watch: {
    switch() {
      if (this.switch[0] == "next") {
        if (this.playingID == null) {
          this.playingID = 0;
          this.$emit("track", this.songs[this.playingID + 1]);
        } else if (this.songs[this.playingID + 1]) {
          this.$emit("track", this.songs[this.playingID + 1]);
          this.playingID++;
        } else if (!("track", this.songs[this.playingID + 1])) {
          this.playingID = 0;
          this.$emit("track", this.songs[this.playingID]);
        }
      }
      if (this.switch[0] == "back") {
        if (this.playingID == null) {
          this.playingID = this.songs.length - 1;
          this.$emit("track", this.songs[this.playingID]);
        } else if (this.songs[this.playingID - 1]) {
          this.playingID--;
          this.$emit("track", this.songs[this.playingID]);
        } else if (this.playingID == 0) {
          this.playingID = this.songs.length - 1;
          this.$emit("track", this.songs[this.playingID]);
        } else if (!this.songs[this.playingID - 1]) {
          this.playingID = 0;
          this.$emit("track", this.songs[this.playingID]);
        }
      }
    },
    playStatus() {
      if (this.isPlay == null) {
        this.playingID = 0;
      }
      this.isPlay = this.playStatus;
    },
  },
  methods: {
    play(track, id) {
      this.$emit("track", track);
      this.playingID = id;
    },
    selectItem(e, item) {
      let songs = this.songs;
      this.songs[item].isSelect = !this.songs[item].isSelect;
      if (!e.ctrlKey && !e.shiftKey) {
        this.songs.forEach(function (i, index) {
          if (i.isSelect && index != item) {
            i.isSelect = false;
          }
        });
      }
      if (e.shiftKey) {
        this.songs.forEach(function (i, index) {
          if (songs[index].isSelect) {
            if (item < index) {
              while (item != index) {
                songs[index].isSelect = true;
                index--;
              }
            } else {
              while (item != index) {
                songs[index].isSelect = true;
                index++;
              }
            }
            return;
          }
        });
        this.songs = songs;
      }
    },
    openContextMenu() {
      this.isContextMenuActive = true;
      this.$emit("context-menu", this.isContextMenuActive);
    },
    getTime(sec) {
      let timestamp = sec;

      let hours = Math.floor(timestamp / 60 / 60);

      let minutes = Math.floor(timestamp / 60) - hours * 60;

      let seconds = timestamp % 60;
      if (seconds < 10) {
        seconds = "0" + seconds;
      }
      let formatted = minutes + ":" + seconds;
      return formatted;
    },
    mouseOverSong(id) {
      this.mouseOver = id;
    },
    mouseLeaveSong() {
      this.mouseOver = null;
    },
  },
};
</script>

<style lang="scss">
.selected-item {
  background: #ffffff44;
}
.selected-item:hover {
  background: #ffffff44 !important;
}
.main {
  &__content {
    padding-top: 100px;
    height: 100%;
  }
  &__background {
    width: 100%;
    height: 1500px;
    background: linear-gradient(180deg, #25aa57 5.09%, #181a20 43.28%);
    position: absolute;
  }
}
.playlist {
  height: 100%;
  &__header {
    padding-left: 30px;
  }
  &__header {
    display: flex;
    align-items: center;
  }
  &__text {
  }
  &__title {
    font-size: 48px;
    font-weight: 700;
  }
  &__info {
    display: flex;
    gap: 15px;
    margin-top: 5px;
    span {
      font-weight: 700;
      font-size: 14px;
    }
  }
  &__main {
    height: 100%;
    width: 100%;
    margin-top: 5px;
    background: rgba(24, 26, 32, 0.1);
    backdrop-filter: blur(30px);
    min-height: 1500px;
  }
  &__control-panel {
    margin-left: 40px;
    padding-top: 30px;
  }
  &__table {
    margin-left: 40px;
    margin-right: 40px;
    margin-top: 30px;
    color: #9c9c9d;
    table {
      width: 100%;
      border-collapse: collapse;
      border-spacing: 0;
      table-layout: fixed;
    }
    th:nth-child(1) {
      width: 5%;
    }
    th:nth-child(2) {
      width: 40%;
    }
    th:nth-child(3) {
      width: 30%;
    }
    th:nth-child(4) {
      width: 20%;
    }

    td:first-child,
    th:first-child {
      border-radius: 6px 0 0 6px;
    }
    td:last-child,
    th:last-child {
      border-radius: 0 6px 6px 0;
    }
    tr:not(:first-child):hover {
      background: #ffffff18;
    }

    th {
      padding-bottom: 10px;
      span:hover {
        color: white;
      }

      border-bottom: 1px solid #666666;
      font-size: 16px;
    }
  }
}
.play-btn {
}
.album {
  a {
    color: white;
  }
  a:hover {
    text-decoration: underline;
  }
}
.sep {
  width: 2px;
  height: 14px;
  background-color: white;
  border-radius: 1px;
}
.circle-big {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 72px;
  height: 72px;
  border-radius: 50%;
  background: linear-gradient(212.49deg, #10ca52 14.61%, #27e069 87.16%);
  img {
    width: 22px;
    height: 24px;
  }
}
.separator {
  height: 25px;
}
</style>
<style lang="scss" scoped>
.track-info {
  display: flex;
  gap: 20px;
  align-items: center;
  padding-top: 10px;
  padding-bottom: 10px;
  &__img {
    width: 52px;
    height: 52px;

    img {
      width: 100%;
      height: 100%;
      border-radius: 4px;
    }
  }
  &__text {
  }
  &__title {
    a {
      font-size: 20px;
      text-decoration: none;
      color: white;
    }
  }
  &__performer {
    margin-top: 2px;
    a {
      font-size: 18px;
      color: #9c9c9d;
    }
    a:hover {
      text-decoration: underline;
    }
  }
}
.playing {
  .id {
    color: #65d36e;
  }
  .track-info__title {
    a {
      color: #65d36e;
    }
  }
}
</style>
