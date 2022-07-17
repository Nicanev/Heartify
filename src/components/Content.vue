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
                <th align="left">TITLE</th>
                <th align="left">ALBUM</th>
                <th align="left">DATE ADDED</th>
              </tr>
              <tr class="separator" />
              <tr>
                <td align="center">1</td>
                <td valign="middle">
                  <div class="playlist__track-info track-info">
                    <div class="track-info__img">
                      <img src="../static/img/album-image.png" alt="" />
                    </div>
                    <div class="track-info__text">
                      <div class="track-info__title">
                        <a href="#">Testing track</a>
                      </div>
                      <div class="track-info__performer">
                        <a href="#">Test</a>
                      </div>
                    </div>
                  </div>
                </td>
                <td class="album"><a href="#">Test</a></td>
                <td class="date-add">4 ноября 2021 г.</td>
              </tr>
              <tr>
                <td align="center">2</td>
                <td valign="middle">
                  <div class="playlist__track-info track-info">
                    <div class="track-info__img">
                      <img src="../static/img/album-image.png" alt="" />
                    </div>
                    <div class="track-info__text">
                      <div class="track-info__title">
                        <a href="#">Testing track</a>
                      </div>
                      <div class="track-info__performer">
                        <a href="#">Test</a>
                      </div>
                    </div>
                  </div>
                </td>
                <td class="album"><a href="#">Test</a></td>
                <td class="date-add">4 ноября 2021 г.</td>
              </tr>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
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
      padding-bottom: 15px;

      border-bottom: 1px solid #666666;
      font-size: 16px;
    }
  }
}
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
