<template>
  <div class="player__content">
    <div class="player__track-info">Disturbed</div>
    <div class="player__control-panel">Pause</div>
    <div class="player__volume">Volume</div>
  </div>
</template>

<style lang="scss">
.player {
  &__content {
    display: grid;
    align-items: center;
    grid-template-columns: 1fr 1fr 1fr;
  }
  &__track-info {
  }
  &__control-panel {
    justify-self: center;
  }
  &__volume {
    justify-self: end;
  }
}
</style>
