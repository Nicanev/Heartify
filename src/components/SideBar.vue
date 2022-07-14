<template>
  <div class="sidebar__content">
    <div class="sidebar__logo">
      <img src="../static/img/icons/Logo.svg" alt="Logo" />
    </div>
    <div class="sidebar__menu menu">
      <div class="menu__items">
        <div class="menu__item">
          <img src="../static/img/icons/Home.svg" alt="Homepage" />
          <a href="#">Home</a>
        </div>
        <div class="menu__item">
          <img src="../static/img/icons/Search.svg" alt="Search" />
          <a href="#">Search</a>
        </div>
        <div class="menu__item">
          <img src="../static/img/icons/Library.svg" alt="Library" />
          <a href="#">Library</a>
        </div>
      </div>
    </div>
    <div class="sidebar__playlists playlists">
      <div class="playlists__items">
        <div class="playlists__item">
          <div class="circle">
            <img src="../static/img/icons/Cross.svg" />
          </div>
          <a href="#">Add new playlist</a>
        </div>
        <div class="playlists__item">
          <div class="circle">
            <img src="../static/img/icons/Like.svg" />
          </div>
          <a href="#">Liked songs</a>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.sidebar {
  &__content {
    margin-left: 30px;
    margin-top: 20px;
  }
  &__menu {
  }
  &__logo {
    margin-left: -7px;
    margin-bottom: 30px;
  }
}
.playlists {
  margin-top: 40px;
  &__items {
  }
  &__item {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 15px;
    margin-top: 20px;
    cursor: pointer;
    a {
      font-weight: bold;
      font-size: 16px;
      color: #9c9c9d;
      align-self: center;
    }
  }
}
.menu {
  &__items {
  }
  &__item {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 20px;
    margin-top: 20px;
    cursor: pointer;
    a {
      font-weight: bold;
      font-size: 16px;
      letter-spacing: 0.2px;
      color: #9c9c9d;
    }

    img {
      height: 20px;
      width: 20px;
    }
  }
}
.circle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: linear-gradient(212.49deg, #10ca52 14.61%, #27e069 87.16%);
}
</style>
