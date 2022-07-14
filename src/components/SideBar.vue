<template>
  <div class="sidebar__content">
    <div class="sidebar__logo">
      <img src="../static/img/icons/Logo.svg" alt="Logo" />
    </div>
    <div class="sidebar__menu menu">
      <div class="menu__items">
        <div class="menu__item">
          <svg
            width="20"
            height="20"
            viewBox="0 0 71 74"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M39.0492 1.39371C37.9878 0.493888 36.6415 0 35.25 0C33.8585 0 32.5122 0.493888 31.4508 1.39371L2.07583 26.3155C1.42537 26.8669 0.90276 27.5534 0.54429 28.3271C0.185821 29.1009 9.04416e-05 29.9434 0 30.7961V67.6245C0 69.1827 0.618972 70.677 1.72075 71.7788C2.82252 72.8806 4.31685 73.4995 5.875 73.4995H24.4792C25.2582 73.4995 26.0054 73.1901 26.5563 72.6392C27.1072 72.0883 27.4167 71.3411 27.4167 70.562V46.0829H43.0833V70.562C43.0833 72.1835 44.3993 73.4995 46.0208 73.4995H64.625C66.1831 73.4995 67.6775 72.8806 68.7793 71.7788C69.881 70.677 70.5 69.1827 70.5 67.6245V30.7961C70.4999 29.9434 70.3142 29.1009 69.9557 28.3271C69.5972 27.5534 69.0746 26.8669 68.4242 26.3155L39.0492 1.39371V1.39371Z"
              fill="#9C9C9D"
            />
          </svg>

          <a href="#">Home</a>
        </div>
        <div class="menu__item">
          <svg
            width="20"
            height="20"
            viewBox="0 0 20 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M19.7479 18.5745L14.0096 12.8274C15.1409 11.4696 15.8213 9.73439 15.8213 7.8392C15.8213 3.51554 12.2758 0 7.91475 0C3.55364 0 0 3.51964 0 7.8433C0 12.167 3.54545 15.6825 7.90655 15.6825C9.7592 15.6825 11.4643 15.0467 12.8169 13.9842L18.5757 19.7477C18.9118 20.0841 19.4118 20.0841 19.7479 19.7477C20.084 19.4113 20.084 18.9109 19.7479 18.5745ZM1.6805 7.8433C1.6805 4.44672 4.47587 1.68598 7.90655 1.68598C11.3372 1.68598 14.1326 4.44672 14.1326 7.8433C14.1326 11.2399 11.3372 14.0006 7.90655 14.0006C4.47587 14.0006 1.6805 11.2358 1.6805 7.8433Z"
              fill="#9C9C9D"
            />
          </svg>
          <a href="#">Search</a>
        </div>
        <div class="menu__item">
          <svg
            width="20"
            height="20"
            viewBox="0 0 20 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M5.42299 0.833333L6.10087 0H8.81236L9.49024 0.833333V19.1667L8.81236 20H6.10087L5.42299 19.1667V0.833333ZM6.77874 1.66667V18.3333H8.13449V1.66667H6.77874ZM11.0778 2.24167L11.4832 1.17333L14.032 0.0333333L14.8997 0.531667L20 17.7583L19.5946 18.8267L17.0472 19.9667L16.1795 19.4683L11.0765 2.24167H11.0778ZM12.5827 2.455L17.2194 18.115L18.4938 17.5467L13.8571 1.885L12.5827 2.455V2.455ZM0 0.833333L0.677874 0H3.38937L4.06725 0.833333V19.1667L3.38937 20H0.677874L0 19.1667V0.833333ZM1.35575 1.66667V18.3333H2.7115V1.66667H1.35575Z"
              fill="#9C9C9D"
            />
          </svg>

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
    cursor: pointer;
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
  &__item:hover {
    a {
      color: white;
      transition: 0.2s;
    }
    .circle {
      box-shadow: inset 0px 0px 25px rgba(255, 255, 255, 0.4);
      transition: 0.2s;
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
  }
  &__item:hover {
    a {
      color: white;
      transition: 0.2s;
    }
    svg path {
      fill: white;
      transition: 0.2s;
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
