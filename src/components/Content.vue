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
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.main {
  &__content {
    padding-top: 100px;
    padding-left: 30px;
  }
  &__background {
    width: 100%;
    height: 1500px;
    background: linear-gradient(180deg, #25aa57 5.09%, #181a20 43.28%);
    position: absolute;
  }
}
.playlist {
  &__header {
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
}
.sep {
  width: 2px;
  height: 14px;
  background-color: white;
  border-radius: 1px;
}
</style>
