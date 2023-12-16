<script lang="ts" setup>
import { ref, reactive, onMounted } from 'vue';

const inputs = ref<HTMLElement[]>([]);

const inputValues:number[] = reactive([
  null,
  null,
  null,
  null
]);

const isNumber = (event: KeyboardEvent) => {
  const value = parseInt(event.key);
  if (isNaN(value)) {
    event.preventDefault();
  }
};

const handleKeydown = ({ event, index }) => {
  const value = parseInt(event.key);

  if (!isNaN(value)) {
    inputValues[index] = value;
    moveToNextInput(index);
  } else if (event.key === 'Backspace') {
    inputValues[index] = null;
    focusInputByIndex(index - 1);
  }
}

const focusInputByIndex = (index: number): void => {
  if (index < 0 || index >= inputs.value.length) {
    return;
  }
  inputs.value[index].focus();
};

const moveToNextInput = (index: number): void => {
  if (index < inputs.value.length - 1) {
    focusInputByIndex(index + 1);
  }
};

const handlePaste = (event: ClipboardEvent): void => {
  const pastedText = event.clipboardData.getData('text');
  const pastedNumbers = pastedText.split('').map(Number);

  const isNumberEvery = pastedNumbers.every((number) => !isNaN(number));
  const isMatchLength = pastedNumbers.length === inputs.value.length;

  if (isMatchLength && isNumberEvery) {
    inputValues.forEach((_, index) => {
      inputValues[index] = pastedNumbers[index];
    });
  } else {
    event.preventDefault();
  }
};

onMounted(() => {
  focusInputByIndex(0);
});
</script>

<template>
  <form>
    <div class="otp-container">
      <h3 class="otp-title">Enter verification</h3>
      <div class="input-group">
        <input
          v-for="(input, index) in inputValues"
          :key="`input_${index}`"
          :value="inputValues[index]"
          ref="inputs"
          class="input"
          type="text"
          maxlength="1"
          @keypress="isNumber($event)"
          @keyup="(event) => handleKeydown({event, index})"
          @paste="handlePaste"
        >
      </div>
    </div>
  </form>
</template>

<style scoped>
.otp-container {
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 1rem;
}
.otp-title {
  font-size: 2rem;
}

.input-group {
  display: flex;
  gap: 1rem;
}

.input-group > .input {
  width: 8rem;
  height: 12rem;
  text-align: center;
  font-size: 2rem;
}
</style>
