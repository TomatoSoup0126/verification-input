<script setup lang="ts">
</script>

<template>
  <div class="loading">
    <div class="loading__container">
      <div class="loading__spinner"/>
      <div class="loading__text">Loading</div>
    </div>
  </div>
</template>

<style scoped>
.loading {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;

  .loading__container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 1rem;
  }

  .loading__spinner {
    width: 5rem;
    height: 5rem;
    border-radius: 50%;
    border: 0.5rem solid #fff;
    border-top-color: #000;
    animation: spin 1s linear infinite;
  }

  .loading__text {
    font-size: 2rem;
    color: #fff;
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}
</style>
