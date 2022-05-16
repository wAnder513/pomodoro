<template>
  <div class="timer-buttons">
    <button
      class="timer-button_start"
      :disabled="hasInputError"
      @click="this.$emit('start-timer')"
    >
      Start
    </button>
    <button class="timer-button_stop" @click="this.$emit('stop-timer')">
      Stop
    </button>
  </div>
</template>

<script>
export default {
  props: {
    hasWarnigMessage: { type: Boolean, default: false },
    inputError: Object
  },
  computed: {
    hasInputError () {
      return (
        this.hasWarnigMessage ||
        this.inputError.hasInputErrorWork ||
        this.inputError.hasInputErrorRelax
      )
    }
  }
}
</script>

<style scoped>
.timer-buttons {
  display: flex;
  justify-content: space-between;
}

.timer-button_start {
  background-color: greenyellow;
}

.timer-button_start:disabled {
  background-color: rgb(126, 136, 111);
  cursor: not-allowed;
}

.timer-button_stop {
  background-color: rgb(70, 80, 1);
}
</style>
