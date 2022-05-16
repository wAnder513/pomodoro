<template>
  <div class="timer-settings">
    <div>
      <span class="timer-settings_text">Work</span>

      <input
        class="timer-settings_input"
        type="number"
        min="1"
        step="1"
        @change="changeSettingsWork"
      />

      <div v-if="inputError.hasInputErrorWork" class="timer-settings_error">
        Invalid value
      </div>
    </div>

    <div>
      <span class="timer-settings_text">Delay</span>

      <input
        class="timer-settings_input"
        type="number"
        min="1"
        step="1"
        @change="changeSettingsDelay"
      />

      <div v-if="inputError.hasInputErrorRelax" class="timer-settings_error">
        Invalid value
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    settingsWork: { type: Number, default: 0 },
    settingsDelay: { type: Number, default: 0 },
    inputError: Object
  },
  methods: {
    changeSettingsWork (e) {
      if (e.target.value > 0) {
        this.$emit('change-work-settings', Number(e.target.value))
      } else {
        this.$emit('has-input-error-work')
      }
    },
    changeSettingsDelay (e) {
      if (e.target.value > 0) {
        this.$emit('change-delay-settings', Number(e.target.value))
      } else {
        this.$emit('has-input-error-relax')
      }
    }
  }
}
</script>

<style scoped>
.timer-settings {
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
}

.timer-settings_text {
  margin-right: 5px;
}

.timer-settings_input {
  padding: 0 5px;
  color: black;
  width: 120px;
}

.timer-settings_error {
  color: rgb(0, 14, 139);
  margin-bottom: 10px;
  font-size: 22px;
  text-align: right;
}
</style>
