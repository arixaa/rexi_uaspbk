<template>
  <div class="stopwatch-widget">
    <h2>{{ title }}</h2>
    <div class="stopwatch">
      <p>{{ formatTime }}</p>
      <div class="buttons">
        <button @click="startStopwatch" :disabled="isRunning">Start</button>
        <button @click="stopStopwatch" :disabled="!isRunning">Stop</button>
        <button @click="resetStopwatch">Reset</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Widget Stopwatch',
      isRunning: false,
      startTime: null,
      elapsedTime: 0,
      intervalId: null,
    };
  },
  computed: {
    formatTime() {
      const minutes = Math.floor(this.elapsedTime / 60000);
      const seconds = Math.floor((this.elapsedTime % 60000) / 1000);
      const milliseconds = Math.floor((this.elapsedTime % 1000) / 10);

      return `${this.padNumber(minutes)}:${this.padNumber(seconds)}:${this.padNumber(milliseconds)}`;
    },
  },
  methods: {
    padNumber(number) {
      return number.toString().padStart(2, '0');
    },
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now() - this.elapsedTime;
        this.intervalId = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
        }, 10);
      }
    },
    stopStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.intervalId);
      }
    },
    resetStopwatch() {
      this.elapsedTime = 0;
    },
  },
  beforeDestroy() {
    clearInterval(this.intervalId);
  },
};
</script>

<style scoped>
.stopwatch-widget {
  text-align: center;
}

.stopwatch {
  margin-top: 20px;
}

.buttons {
  margin-top: 10px;
}

.buttons button {
  margin-right: 10px;
}
</style>
