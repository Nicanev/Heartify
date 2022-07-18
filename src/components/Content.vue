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
              >
                <td class="id" v-if="mouseOver != index" align="center">
                  {{ index + 1 }}
                </td>
                <td class="play-btn" v-if="mouseOver == index" align="center">
                  <svg
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
                </td>
                <td valign="middle">
                  <div class="playlist__track-info track-info">
                    <div class="track-info__img">
                      <img
                        src="../static/img/albums/Ten-Thousand-Fists.jpg"
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
  data() {
    return {
      songs: [
        {
          title: "test",
          perform: "Disturbed",
          album: "Ten Thousand Fists",
          album_img: "Ten-Thousand-Fists.jpg",
          src: "Stricken.mp3",
          date_ad: "4 hours ago",
          duration: 257,
        },
        {
          title: "test2",
          perform: "Disturbed",
          album: "Ten Thousand Fists",
          album_img: "Ten-Thousand-Fists.jpg",
          src: "Stricken.mp3",
          date_ad: "4 hours ago",
          duration: 153,
        },
      ],
      mouseOver: null,
      formatTimeEnd: "",
    };
  },
  methods: {
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
      background: #ffffff2a;
    }

    th {
      padding-bottom: 10px;
      span:hover {
        color: white;
      }

      border-bottom: 1px solid #666666;
      font-size: 16px;
    }
    svg path:hover {
      fill: white;
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
</style>
