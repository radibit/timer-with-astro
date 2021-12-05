<template>
  <div class="ring">
    <svg width="518" height="518" viewBox="0 0 518 518">
      <circle
        stroke-width="9px"
        x="0"
        y="y"
        cx="259"
        cy="259"
        r="254"
        transform="rotate(-90 259 259)"
        :stroke-dasharray="[ringDash, ringCircumference - ringDash]"
      />
    </svg>
  </div>

  <div class="timer">
    <div class="time">
      <div class="minutes">
        <input
          class="u-no-border u-no-background"
          type="number"
          ref="inputMinutes"
          v-model="minutes"
          maxlength="2"
          min="0"
          max="60"
          :disabled="!isEditable"
        />
      </div>
      <div class="colon">:</div>
      <div class="seconds">
        <input
          class="u-no-border u-no-background"
          type="number"
          v-model="seconds"
          maxlength="2"
          min="0"
          max="60"
          :disabled="!isEditable"
        />
      </div>
    </div>
    <button
      class="start u-no-border u-no-background"
      @click="toggleTimer()"
      :disabled="isEditable"
    >
      {{ toggleTimerLabel }}
    </button>
    <button class="settings u-no-border u-no-background" @click="setTime()">
      <img src="images/gear.svg" alt="Settings" />
    </button>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const minutes = ref(15);
    const seconds = ref('00');
    const isStarted = ref(false);
    const isEditable = ref(false);
    const toggleTimerLabel = ref('start');
    const ringCircumference = 1596;
    const percentage = ref(100);
    const ringDash = computed(() => (percentage.value * ringCircumference) / 100);

    let timerInterval;

    const toggleTimer = () => {
      isStarted.value = !isStarted.value;

      if (isStarted.value) {
        toggleTimerLabel.value = 'stop';
        let duration =
          parseInt(minutes.value, 10) * 60 + parseInt(seconds.value, 10);
        let time = duration;

        timerInterval = setInterval(() => {
          let displayMinutes = parseInt(duration / 60, 10);
          let displaySeconds = parseInt(duration % 60, 10);

          minutes.value =
            displayMinutes < 10 ? '0' + displayMinutes : displayMinutes;
          seconds.value =
            displaySeconds < 10 ? '0' + displaySeconds : displaySeconds;

          --duration;
          percentage.value = (duration / time) * 100;

          if (duration < 0) {
            toggleTimer();
          }
        }, 1000);
      } else {
        toggleTimerLabel.value = 'start';
        minutes.value = 15;
        seconds.value = '00';
        percentage.value = 100;
        clearInterval(timerInterval);
      }
    };

    return {
      minutes,
      seconds,
      toggleTimerLabel,
      isStarted,
      isEditable,
      toggleTimer,
      ringDash,
      ringCircumference,
    };
  },
  methods: {
    setTime() {
      this.isEditable = !this.isEditable;

      if (this.isEditable) {
        setTimeout(() => this.$refs.inputMinutes.focus(), 0);
      }
    },
  },
};
</script>

<style lang="scss">
.ring {
  stroke: #09a65a;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;

  circle {
    transition: all 0.5s;
  }

  &.ending circle {
    stroke: #900a0a;
  }
}

.timer {
  align-items: center;
  border-radius: 50%;
  box-shadow: inset 0px 0px 114px rgba(0, 0, 0, 0.45);
  color: var(--color-text);
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  height: 500px;
  width: 500px;
  z-index: 2;
  background: linear-gradient(225deg, #2e2d33, #27262b);
  box-shadow: -41px 41px 82px #252429, 41px -41px 82px #313037;
}

.time {
  display: flex;
  font-family: var(--font-family-primary);
  font-size: 196px;
  margin: 30px auto;
  position: relative;
  top: 30px;
}

input[type='number'] {
  border-bottom: 1px dashed var(--color-text);
  color: var(--color-text);
  font-family: var(--font-family-primary);
  font-size: 196px;
  height: 170px;
  width: 175px;
  padding-left: 10px;
  text-align: center;
  outline: none;

  &:disabled {
    border-bottom: none;
  }
}

.start {
  cursor: pointer;
  font-family: var(--font-family-secondary), sans-serif;
  font-size: 16px;
  letter-spacing: 10px;
  line-height: 20px;
  color: var(--color-text);
  opacity: 0.5;
  text-transform: uppercase;
  margin-bottom: 20px;
  font-weight: 700;

  &:hover {
    opacity: 1;
  }
}

.settings {
  cursor: pointer;
  opacity: 0.3;

  &:hover {
    opacity: 1;
  }
}
</style>
