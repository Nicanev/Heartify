<template>
  <div class="player__content">
    <div class="player__track-info">
      <div class="track-info__img">
        <img src="../static/img/album-image.png" alt="album-image" />
      </div>
      <div class="track-info__description">
        <div class="track-info__title"><a href="#"> Deceiver</a></div>
        <div class="track-info__performer"><a href="#">Disturbed</a></div>
      </div>
    </div>
    <div class="player__control-panel">
      <div class="player__buttons">
        <div class="button-back">
          <svg
            width="15"
            height="15"
            viewBox="0 0 15 15"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g clip-path="url(#clip0_38_51)">
              <path
                d="M4.18771 8.89557L12.5269 14.6316C12.8695 14.8678 13.2259 14.9925 13.531 14.9925C14.2009 14.9925 14.645 14.4306 14.645 13.5265L14.645 1.46574C14.645 1.02406 14.5166 0.655043 14.3262 0.398176C14.1329 0.137785 13.8304 -4.47663e-06 13.5037 -4.47663e-06C13.1987 -4.47663e-06 12.8564 0.124905 12.5139 0.360751L4.18224 6.09676C3.64663 6.4659 3.35295 6.96275 3.35307 7.49641C3.35307 8.02983 3.65137 8.52667 4.18771 8.89557Z"
                fill="#BABABA"
              />
              <path
                d="M1.13442 0.00376239L1.14343 0.00387573C1.14491 0.00387573 1.14635 0.00376239 1.14783 0.00376239L1.13442 0.00376239Z"
                fill="#BABABA"
              />
              <path
                d="M1.15912 15L1.50384 14.999C1.95524 14.999 2.34601 14.6311 2.34601 14.1791L2.34601 0.83245C2.34601 0.379955 1.96168 0.00850674 1.50967 0.00850674L1.14348 0.0038892C0.693747 0.00628898 0.354984 0.380928 0.354984 0.831721L0.354984 14.1799C0.354984 14.632 0.707356 15 1.15912 15Z"
                fill="#BABABA"
              />
            </g>
            <defs>
              <clipPath id="clip0_38_51">
                <rect
                  width="15"
                  height="15"
                  fill="white"
                  transform="translate(15 15) rotate(-180)"
                />
              </clipPath>
            </defs>
          </svg>
        </div>
        <div class="circle button-play" @click="play">
          <img v-if="!isPlay" src="../static/img/icons/Play.svg" alt="Play" />
          <img v-if="isPlay" src="../static/img/icons/Pause.svg" alt="Pause" />
        </div>
        <div class="button-next">
          <svg
            width="15"
            height="15"
            viewBox="0 0 20 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g clip-path="url(#clip0_38_26)">
              <path
                d="M14.4164 8.13923L3.29749 0.491211C2.84062 0.176263 2.36545 0.0100403 1.95864 0.0100403C1.06548 0.0100403 0.473328 0.759175 0.473328 1.96469V18.0457C0.473328 18.6346 0.644572 19.1266 0.898442 19.4691C1.1562 19.8163 1.55944 20 1.99509 20C2.40174 20 2.85812 19.8335 3.31483 19.519L14.4237 11.871C15.1378 11.3788 15.5294 10.7163 15.5293 10.0048C15.5293 9.29355 15.1315 8.63109 14.4164 8.13923Z"
                fill="#BABABA"
              />
              <path
                d="M18.4883 19.9949L18.4757 19.9948C18.4737 19.9948 18.4716 19.9949 18.4696 19.9949H18.4883Z"
                fill="#BABABA"
              />
              <path
                d="M18.4545 0L17.9949 0.00129608C17.393 0.00129608 16.872 0.491863 16.872 1.09454V18.8901C16.872 19.4934 17.3844 19.9887 17.9871 19.9887L18.4754 19.9948C19.075 19.9916 19.5267 19.4921 19.5267 18.891V1.09341C19.5267 0.490729 19.0568 0 18.4545 0Z"
                fill="#BABABA"
              />
            </g>
            <defs>
              <clipPath id="clip0_38_26">
                <rect width="20" height="20" fill="white" />
              </clipPath>
            </defs>
          </svg>
        </div>
      </div>
      <div class="player__progressbar">
        <div class="player__time-start time">{{ formatTimeStartTest }}</div>
        <div class="player__slider-container">
          <input
            type="range"
            name="progress-bar"
            id="progress-bar"
            class="slider"
            min="0"
            max="100"
            @click="rewind"
            v-model="statusSong"
          />
          <div
            class="progress-track"
            :style="{ width: 'calc(' + statusSong + '%' + ')' }"
          ></div>
        </div>
        <div class="player__time-end time">{{ formatTimeEnd }}</div>
      </div>
    </div>
    <div class="player__volume">Volume</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      songs: [{ title: "test", duration: 247 }],
      statusSong: 0,
      isPlay: false,
      formatTimeEnd: "",
      formatTimeStart: "0:00",
      audio: "",
      durationSec: "0",
      rewindStatus: false,
    };
  },
  mounted() {
    this.formatTimeEnd = this.getTime(this.songs[0].duration);
    this.audio = new Audio();
    this.audio.src = "src/static/disturbed-stricken.mp3";
  },
  computed: {
    formatTimeStartTest() {
      this.durationSec = (this.statusSong * this.songs[0].duration) / 100;
      this.formatTimeStart = this.getTime(Math.ceil(this.durationSec));
      return this.getTime(Math.ceil(this.durationSec));
    },
  },
  watch: {
    isPlay() {
      let updateTime = setInterval(() => {
        let nowTime =
          (Math.ceil(this.audio.currentTime) * 100) / this.songs[0].duration;
        if (this.rewindStatus) {
          this.audio.currentTime = this.durationSec;
          this.rewindStatus = false;
        } else {
          this.statusSong = nowTime;
        }
      }, 250);
    },
  },
  methods: {
    play() {
      if (!this.isPlay) {
        this.audio.play();
        this.isPlay = true;
      } else {
        this.pause();
      }
    },
    pause() {
      this.audio.pause();
      this.isPlay = false;
    },
    rewind() {
      this.rewindStatus = true;
    },
    getTime(sec) {
      let timestamp = sec;

      let hours = Math.floor(timestamp / 60 / 60);

      let minutes = Math.floor(timestamp / 60) - hours * 60;

      let seconds = timestamp % 60;

      let formatted = minutes + ":" + seconds;
      return formatted;
    },
  },
};
</script>

<style lang="scss">
.player {
  &__content {
    display: grid;
    align-items: center;
    grid-template-columns: 1fr 1fr 1fr;
  }
  &__buttons {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 25px;
  }
  &__slider-container {
    width: 530px;
    position: relative;
  }
  &__progressbar {
    display: flex;
    align-items: center;
    gap: 10px;
    #progress-bar {
      appearance: none;
      height: 8px;
      width: 100%;
      background: #35383e;
      border-radius: 6px;
    }
    .progress-track {
      position: absolute;
      top: 9px;
      appearance: none;
      height: 8px;
      left: 0px;
      z-index: 99;
      pointer-events: none;
      background: linear-gradient(90deg, #2de66f 0%, #18d25b 100%);
      border-radius: 6px;
    }
    #progress-bar::-webkit-slider-thumb {
      appearance: none;
      position: relative;
      z-index: 100;
      width: 15px;
      height: 15px;
      border-radius: 50%;
      background: linear-gradient(90deg, #2ae46d 0%, #0fca52 100%);
      cursor: pointer;
    }
  }
  &__track-info {
    display: flex;
    align-items: center;
    gap: 15px;
    padding-left: 20px;
  }
  &__control-panel {
    justify-self: center;
    display: grid;
    grid-template-columns: auto;
    justify-items: center;
    gap: 5px;
  }
  &__volume {
    justify-self: end;
  }
}
.button-next:hover {
  cursor: pointer;
  svg path {
    fill: white;
    transition: 0.2s;
  }
}
.button-back:hover {
  cursor: pointer;
  svg path {
    fill: white;
    transition: 0.2s;
  }
}
.track-info {
  &__img {
    cursor: pointer;
  }
  &__description {
    display: grid;
    grid-template-columns: auto;
    align-items: center;

    font-weight: bold;
  }
  &__title {
    a {
      font-size: 16px;
      text-decoration: none;
      color: white;
    }
    a:hover {
      text-decoration: underline;
    }
  }
  &__performer {
    a {
      font-size: 12px;
      color: #9c9c9d;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
      color: white;
    }
  }
}
.circle {
  display: flex;
  align-items: center;
  cursor: pointer;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: linear-gradient(212.49deg, #10ca52 14.61%, #27e069 87.16%);
  box-sizing: border-box;
}
.circle:active {
  transform: scale(0.95);
  transition: 0.2s;
}
.time {
  margin-top: 5px;
  font-size: 14px;
}
</style>
