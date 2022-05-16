<template>
  <div class="app_wrapper" :class="workingTime">
    <timer-main
      :isWorkingTime="isWorkingTime"
      :minuts="minuts"
      :seconds="seconds"
      :isTimerOn="isTimerOn"
      @change-timer="changeTimer"
      @change-status="changeStatus"
    >
    </timer-main>
    <timer-settings
      :settings-work="settingsWork"
      :settings-delay="settingsDelay"
      :inputError="inputError"
      @has-input-error-work="hasInputErrorWork"
      @has-input-error-relax="hasInputErrorRelax"
      @change-work-settings="changeSettingsWork"
      @change-delay-settings="changeSettingsDelay"
    ></timer-settings>
    <div v-if="hasWarnigMessage">Fill in all the fields</div>
    <timer-buttons
      :hasWarnigMessage="hasWarnigMessage"
      :inputError="inputError"
      @start-timer="startTimer"
      @stop-timer="stopTimer"
    ></timer-buttons>
  </div>
</template>

<script>
import TimerButtons from './components/TimerButtons.vue'
import TimerMain from './components/TimerMain.vue'
import TimerSettings from './components/TimerSettings.vue'

export default {
  name: 'App',
  components: { TimerMain, TimerSettings, TimerButtons },
  data () {
    return {
      isWorkingTime: true,
      minuts: 0,
      seconds: 0,
      settingsWork: null,
      settingsDelay: null,
      isTimerOn: false,
      inputError: {
        hasInputErrorWork: false,
        hasInputErrorRelax: false
      }
    }
  },
  computed: {
    workingTime () {
      return this.isWorkingTime ? 'working-time' : 'delay-time'
    },
    hasWarnigMessage () {
      return this.settingsWork === null || this.settingsDelay === null
    }
  },
  methods: {
    changeTimer () {
      if (this.seconds !== 0) {
        this.seconds -= 1
      } else {
        this.seconds = 59
        this.minuts -= 1
      }
    },
    changeSettingsWork (changeMinutsValueWork) {
      this.settingsWork = changeMinutsValueWork
      this.inputError.hasInputErrorWork = false
    },
    changeSettingsDelay (changeMinutsValuDelay) {
      this.settingsDelay = changeMinutsValuDelay
      this.inputError.hasInputErrorRelax = false
    },
    changeStatus () {
      this.isWorkingTime = !this.isWorkingTime
      this.minuts = this.settingsDelay
      this.seconds = 0
    },
    startTimer () {
      this.isTimerOn = true
      this.minuts = this.settingsWork
      this.seconds = 0
    },
    stopTimer () {
      this.isTimerOn = false
    },
    hasInputErrorWork () {
      this.inputError.hasInputErrorWork = true
    },
    hasInputErrorRelax () {
      this.inputError.hasInputErrorRelax = true
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-size: 40px;
  color: #fff;
}

button {
  border: none;
  cursor: pointer;
  padding: 0 10px;
  font-size: 30px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 200px;
}

.app_wrapper {
  padding: 20px 60px;
  max-width: 600px;
  margin: 0 auto;
}

.working-time {
  background-color: rgb(123, 15, 15);
}

.delay-time {
  background-color: rgb(17, 170, 71);
}
</style>
