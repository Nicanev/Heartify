<template>
  <div class="player__content">
    <div class="player__track-info" v-if="track">
      <div class="track-info__img">
        <img
          :src="'/src/static/img/albums/' + track.album_img"
          alt="album-image"
        />
      </div>
      <div class="track-info__description">
        <div class="track-info__title">
          <a href="#" v-if="track"> {{ track.title }}</a>
        </div>
        <div class="track-info__performer">
          <a href="#">{{ track.perform }}</a>
        </div>
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
        <div class="circle button-play" @click="playSong">
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
        <div class="player__time-start time">
          {{ formatTimeStartUpdate }}
        </div>
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
    <div class="player__volume volume">
      <div class="volume__icon" @click="mute">
        <svg
          v-if="statusVolume > 0 && statusVolume < 70"
          width="28"
          height="28"
          viewBox="0 0 28 28"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M15.7117 4.73972C15.6835 4.5659 15.4671 4.47296 15.3137 4.62495L12.0842 7.826C11.0073 8.89337 9.54604 9.49312 8.02227 9.49312C7.76985 9.49312 7.56522 9.69572 7.56522 9.94564V14.0544C7.56522 14.3043 7.76985 14.5069 8.02227 14.5069C9.54604 14.5069 11.0073 15.1066 12.0842 16.174L15.3137 19.3751C15.4671 19.527 15.6835 19.4341 15.7117 19.2603C16.0244 17.3313 16.4348 14.3455 16.4348 12C16.4348 9.65454 16.0244 6.66871 15.7117 4.73972ZM14.2064 3.52973C15.235 2.51017 17.0202 3.03295 17.2571 4.4941C17.5715 6.43286 18 9.52248 18 12C18 14.4775 17.5715 17.5671 17.2571 19.5059C17.0202 20.967 15.235 21.4898 14.2064 20.4703L10.9768 17.2692C10.1935 16.4928 9.13062 16.0566 8.02227 16.0566C6.9054 16.0566 6 15.1602 6 14.0544V9.94564C6 8.83984 6.9054 7.94341 8.02227 7.94341C9.13062 7.94341 10.1935 7.50717 10.9768 6.73079L14.2064 3.52973Z"
            fill="#BABABA"
          />
          <path
            d="M19 9C20.2806 9.79573 21 10.8748 21 12C21 13.1252 20.2806 14.2043 19 15"
            stroke="#BABABA"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
        <svg
          v-if="statusVolume >= 70"
          width="28"
          height="28"
          viewBox="0 0 28 28"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M13.7117 4.73972C13.6835 4.5659 13.4671 4.47296 13.3137 4.62495L10.0842 7.826C9.0073 8.89337 7.54604 9.49312 6.02227 9.49312C5.76985 9.49312 5.56522 9.69572 5.56522 9.94564V14.0544C5.56522 14.3043 5.76985 14.5069 6.02227 14.5069C7.54604 14.5069 9.0073 15.1066 10.0842 16.174L13.3137 19.3751C13.4671 19.527 13.6835 19.4341 13.7117 19.2603C14.0244 17.3313 14.4348 14.3455 14.4348 12C14.4348 9.65454 14.0244 6.66871 13.7117 4.73972ZM12.2064 3.52973C13.235 2.51017 15.0202 3.03295 15.2571 4.4941C15.5715 6.43286 16 9.52248 16 12C16 14.4775 15.5715 17.5671 15.2571 19.5059C15.0202 20.967 13.235 21.4898 12.2064 20.4703L8.9768 17.2692C8.1935 16.4928 7.13062 16.0566 6.02227 16.0566C4.9054 16.0566 4 15.1602 4 14.0544V9.94564C4 8.83984 4.9054 7.94341 6.02227 7.94341C7.13062 7.94341 8.1935 7.50717 8.9768 6.73079L12.2064 3.52973Z"
            fill="#BABABA"
          />
          <path
            d="M17 9C18.2806 9.79573 19 10.8748 19 12C19 13.1252 18.2806 14.2043 17 15"
            stroke="#BABABA"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
          <path
            d="M18 7C19.9209 8.32622 21 10.1247 21 12C21 13.8753 19.9209 15.6738 18 17"
            stroke="#BABABA"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
        <svg
          v-if="statusVolume == 0"
          width="28"
          height="28"
          viewBox="0 0 28 28"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M13.7117 4.73972C13.6835 4.5659 13.4671 4.47296 13.3137 4.62495L10.0842 7.826C9.0073 8.89337 7.54604 9.49312 6.02227 9.49312C5.76985 9.49312 5.56522 9.69572 5.56522 9.94564V14.0544C5.56522 14.3043 5.76985 14.5069 6.02227 14.5069C7.54604 14.5069 9.0073 15.1066 10.0842 16.174L13.3137 19.3751C13.4671 19.527 13.6835 19.4341 13.7117 19.2603C14.0244 17.3313 14.4348 14.3455 14.4348 12C14.4348 10.3176 14.2236 8.30568 13.9888 6.59068C13.8963 5.9148 13.8001 5.28503 13.7117 4.73972ZM12.2064 3.52973C13.235 2.51017 15.0202 3.03295 15.2571 4.4941C15.5715 6.43286 16 9.52248 16 12C16 14.4775 15.5715 17.5671 15.2571 19.5059C15.0202 20.967 13.235 21.4898 12.2064 20.4703L8.9768 17.2692C8.1935 16.4928 7.13062 16.0566 6.02227 16.0566C4.9054 16.0566 4 15.1602 4 14.0544V9.94564C4 8.83984 4.9054 7.94341 6.02227 7.94341C7.13062 7.94341 8.1935 7.50717 8.9768 6.73079L12.2064 3.52973Z"
            fill="#BABABA"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M17.2375 14.6458C17.1063 14.5226 17.1014 14.318 17.2265 14.1889L22.0247 9.2339C22.1498 9.10472 22.3575 9.09986 22.4887 9.22305C22.6199 9.34624 22.6248 9.55082 22.4997 9.68L17.7015 14.635C17.5764 14.7641 17.3687 14.769 17.2375 14.6458Z"
            fill="#B3B3B3"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M22.6355 14.6458C22.7667 14.5226 22.7716 14.318 22.6465 14.1889L17.8483 9.2339C17.7232 9.10472 17.5155 9.09986 17.3843 9.22305C17.2531 9.34624 17.2482 9.55082 17.3733 9.68L22.1715 14.635C22.2966 14.7641 22.5044 14.769 22.6355 14.6458Z"
            fill="#B3B3B3"
          />
        </svg>
      </div>
      <div class="volume__progressbar">
        <div class="volume__slider-container">
          <input
            type="range"
            name="volume-track"
            id="volume-track"
            v-model="statusVolume"
            min="0"
            max="100"
            step="10"
          />
          <div
            class="progress-volume"
            :style="{ width: statusVolume + '%' }"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["track"],
  data() {
    return {
      songs: [{ title: "test", duration: 153 }],
      statusSong: 0,
      statusVolume: 20,
      isPlay: false,
      formatTimeEnd: "",
      formatTimeStart: "0:00",
      audio: "",
      durationSec: "0",
      rewindStatus: false,
    };
  },
  mounted() {
    this.formatTimeEnd = this.getTime(this.track.duration);
    this.audio = new Audio();
    this.audio.src = "src/static/music/" + this.track.src;
  },
  computed: {
    formatTimeStartUpdate() {
      this.durationSec = (this.statusSong * this.track.duration) / 100;
      if (this.durationSec >= this.audio.duration) {
        this.durationSec = this.durationSec - 1;
        this.pause();
      }
      this.formatTimeStart = this.getTime(Math.ceil(this.durationSec));

      return this.getTime(Math.ceil(this.durationSec));
    },
  },
  watch: {
    isPlay() {
      let updateTime = setInterval(() => {
        let nowTime =
          (Math.ceil(this.audio.currentTime) * 100) / this.track.duration;
        if (this.rewindStatus) {
          this.audio.currentTime = this.durationSec;
          this.rewindStatus = false;
        } else {
          this.statusSong = nowTime;
        }
      }, 1000);
    },
    statusVolume() {
      this.audio.volume = this.statusVolume / 100;
    },
    track() {
      if (this.track) {
        this.formatTimeEnd = this.getTime(this.track.duration);
      }
    },
  },
  methods: {
    playSong() {
      if (!this.isPlay) {
        this.audio.play();
        this.audio.volume = this.statusVolume / 100;
        this.isPlay = true;
      } else {
        this.pause();
      }
    },
    pause() {
      this.audio.pause();
      this.isPlay = false;
    },
    mute() {
      this.statusVolume = 0;
    },
    rewind() {
      this.rewindStatus = true;
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
      display: none;
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
  &__progressbar:hover {
    #progress-bar::-webkit-slider-thumb {
      display: block;
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

.volume {
  display: flex;
  align-items: center;
  padding-right: 20px;
  gap: 5px;
  &__icon {
    margin-top: 10px;
    cursor: pointer;
  }
  &__slider-container {
    width: 100px;
    position: relative;
  }
  &__progressbar {
    input {
      appearance: none;
      height: 8px;
      width: 100%;
      background: #35383e;
      border-radius: 6px;
    }
    input::-webkit-slider-thumb {
      appearance: none;
      position: relative;
      z-index: 100;
      width: 15px;
      height: 15px;
      border-radius: 50%;
      background: transparent;
      cursor: pointer;
      transition: 0.2s;
    }
    .progress-volume {
      position: absolute;
      top: 9px;
      appearance: none;
      height: 8px;
      left: 0px;
      width: 20%;
      z-index: 99;
      pointer-events: none;
      background: linear-gradient(90deg, #2de66f 0%, #18d25b 100%);
      border-radius: 6px;
    }
  }
}
.volume:hover {
  input::-webkit-slider-thumb {
    background: linear-gradient(90deg, #2ae46d 0%, #0fca52 100%);
    transition: 0.2s;
  }
  svg path {
    fill: white;
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
<style lang="scss" scoped>
.track-info {
  &__img {
    cursor: pointer;
    img {
      width: 60px;
      height: 60px;
      border-radius: 4px;
    }
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
</style>
