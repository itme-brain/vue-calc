<template>
  <div class="calculator">
    <div class="display">{{ result }}</div>
    <div class="buttons">
      <button v-for="button in buttons" :key="button" @click="handleClick(button)">
        {{ button }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      result: '',
      buttons: ['1', '2', '3', '4', '5', '6', '7', '8', '9', ' ', '0', ' ', '+', '-', '*', '/', '=', 'C'],
    };
  },
  methods: {
    handleClick(button) {
      switch (button) {
        case '=':
          this.evaluateExpression();
          break;
        case 'C':
          this.clearDisplay();
          break;
        default:
          this.appendButtonValue(button);
          break;
      }
    },

    evaluateExpression() {
      try {
        this.result = eval(this.result);
      } catch (error) {
        this.showError();
      }
    },

    clearDisplay() {
      this.result = '';
    },

    appendButtonValue(button) {
      this.result += button;
    },

    showError() {
      this.result = 'Error';
    },
  },
};
</script>

<style scoped>
.calculator {
  @apply w-40 mx-auto text-center;
}

.display {
  @apply h-10 mb-2 flex items-center justify-center text-2xl;
}

.buttons {
  @apply grid grid-cols-3 bg-sky-500 gap-2;
}

button {
  @apply px-4 py-2 bg-red-200 border-none cursor-grab text-xl;
}
</style>
