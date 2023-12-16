<script lang="ts" setup>
import { ref, reactive, onMounted } from 'vue';

const inputs = ref<HTMLElement[]>([]);

const inputValues = reactive<number | null[]>([
  null,
  null,
  null,
  null
]);

const step:number = ref(0)

const focusInputByIndex = (index: number): void => {
  if (index < inputs.value.length) {
    inputs.value[index].focus();
  }
};

const moveToNextInput = (index: number): void => {
  if (index < inputs.value.length - 1) {
    focusInputByIndex(index + 1);
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
            class="input"
            ref="inputs"
            type="text"
            v-model="inputValues[index]"
            @input="moveToNextInput(index)"
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
