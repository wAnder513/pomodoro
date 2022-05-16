<template>
  <div class="timer-main">
    <div class="timer-main_text">{{ periodText }}</div>
    <div>
      <span v-if="minuts < 10">0</span>{{ minuts }}:<span v-if="seconds < 10"
        >0</span
      >{{ seconds }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'TimerMain',
  data () {
    return {}
  },
  props: {
    isWorkingTime: { type: Boolean, default: true },
    isTimerOn: { type: Boolean, default: false },
    minuts: { type: Number, default: 0 },
    seconds: { type: Number, default: 0 }
  },
  mounted () {},
  computed: {
    periodText () {
      return this.isWorkingTime ? 'Working time now' : 'Time to relax'
    }
  },
  methods: {
    timer () {
      const timeout = setInterval(() => {
        if (this.isTimerOn) {
          if (this.minuts === 0 && this.seconds === 0) {
            this.$emit('change-status')
          } else {
            this.$emit('change-timer')
          }
        } else {
          clearInterval(timeout)
        }
      }, 1000)
    }
  },
  watch: {
    isTimerOn: function () {
      this.timer()
    }
  }
}
</script>

<style scoped>
.timer-main {
  margin-bottom: 50px;
}

.timer-main_text {
  margin-bottom: 20px;
}
</style>
