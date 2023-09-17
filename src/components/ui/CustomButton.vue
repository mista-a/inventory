<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<style scoped>
.button {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  border: 0;
  padding: 0;
  cursor: pointer;
  background: inherit;
}
.button:active {
  transform: scale(0.97);
}
</style>
