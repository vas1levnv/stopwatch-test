<template>
  <div class="stopwatch-page-item timer"
       :class="{active: isPlayTimer}"
  >
    <div class="timer-text">
      <span v-show="hours">{{ hours }}</span>
      <span v-show="hours">:</span>
      <span v-show="minutes">
        <span v-show="isMinutesZero">0</span>
        <span>{{ minutes }}</span>
      </span>
      <span v-show="minutes">:</span>
      <span>{{ time }}</span>
    </div>
    <div class="timer-border"></div>
    <div class="timer-btn">
      <button @click="playTimer"
              v-show="!isPlayTimer"
              class="btn"
      >
        <svg width="17" height="20" viewBox="0 0 17 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E"/>
        </svg>

      </button>
      <button @click="stopTimer"
              v-show="isPlayTimer"
              class="btn"
      >
        <svg width="10" height="20" viewBox="0 0 10 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="7" width="3" height="20" fill="#9E9E9E"/>
          <rect width="3" height="20" fill="#9E9E9E"/>
        </svg>


      </button>
      <button
          @click="resetTimer"
          class="btn"
      >
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect width="20" height="20" fill="#9E9E9E"/>
        </svg>
      </button>


    </div>
  </div>
</template>

<script>
export default {
  props: {},


  data() {
    return {
      time: 0,
      minutes: 0,
      isMinutesZero: true,
      hours: 0,
      isPlayTimer: false,
      timer: null,
    }
  },

  watch: {},

  methods: {
    playTimer() {
      this.timer = setInterval(() => {
        this.time++
        if (this.time <= 9) {
          return;
        }
        this.minutes++
        this.time = 0
        if (this.minutes > 9) {
          this.isMinutesZero = false
        }
        if (this.minutes <= 59) {
          return;
        }
        this.hours++
        this.minutes = 0
      }, 10)
      this.isPlayTimer = true
    },
    stopTimer() {
      clearInterval(this.timer)
      this.isPlayTimer = false
    },
    resetTimer() {
      this.stopTimer()
      this.time = 0
      this.minutes = 0
      this.hours = 0
      this.isMinutesZero = true
    }
  }
}
</script>

<style scoped lang="scss">
@import "../assets/variables";

.timer {
  transition: $tr;

  &-text {
    padding-bottom: 0.75rem;
  }

  &-btn {
    padding-top: 0.75rem;
    display: flex;
    justify-content: space-evenly;
    width: 80%;

    & svg {
      & path, & rect {
        transition: $tr;
      }
    }
  }

  &-border {
    width: 100%;
    height: 2px;
    background: $main-gray;


  }

  &.active {
    color: white;

    & .timer-border {
      background: white;
    }

    & svg {
      & path, & rect {
        fill: white;
      }
    }
  }
}

</style>