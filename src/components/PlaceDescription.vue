<script setup lang="ts">
import ImagePlaceholder from '../assets/temp/place-image-placeholder.png'
</script>

<template>
  <div class="place-description">
    <img :src="ImagePlaceholder" alt="place" class="place-img" />
    <h2 class="place-name">Арктика</h2>
    <p class="place-about">Холодное местечко</p>
  </div>
</template>

<style scoped>
.place-description {
  display: flex;
  width: 236px;
  padding: 18px 14px 24px;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  border-radius: 12px;
  border: 1px solid #4d4d4d;
  background: #262626;
}
.place-img {
  height: 240px;
}
.place-about {
  flex: 1;
  overflow-y: auto;
}
</style>
