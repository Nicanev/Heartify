<template>
  <div class="header__content">
    <div class="header__account">
      <img src="../static/img/Avatar.png" /><a>Nicanev</a>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.header {
  &__content {
    display: grid;
    padding-top: 10px;
    padding-bottom: 10px;
    height: max-content;
  }
  &__account {
    display: flex;
    align-items: center;
    gap: 15px;
    height: max-content;
    padding: 5px 30px 5px 5px;
    justify-self: end;
    margin-right: 20px;
    background-color: black;
    border-radius: 17px;
    cursor: pointer;
    a {
      font-weight: bold;
      font-size: 16px;
    }
  }
  &__account:hover {
    background-color: #282828;
    transition: 0.2s;
  }
}
</style>
