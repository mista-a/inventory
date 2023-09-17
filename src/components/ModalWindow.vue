<script setup lang="ts">
interface ModalWindowProps {
  active: boolean
  position?: 'top' | 'right' | 'bottom' | 'left'
  animationDuration?: number
}

interface ModalWindowEmit {
  (e: 'close'): void
}

defineProps<ModalWindowProps>()
defineEmits<ModalWindowEmit>()
</script>

<template>
  <div v-if="active" class="modal" :style="{ animationDuration: `${animationDuration}s` }">
    <slot></slot>
  </div>
</template>

<style>
@keyframes slidein {
  from {
    max-width: 0;
  }
  to {
    max-width: 100%;
  }
}
.modal {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 4;
  height: 100%;
  animation-name: slidein;
}
</style>
