<script setup lang="ts">
import ItemIcon1 from '@/assets/temp/item-icons/item-icon-1.png'
import ItemIcon2 from '@/assets/temp/item-icons/item-icon-2.png'
import ItemIcon3 from '@/assets/temp/item-icons/item-icon-3.png'
import { type ItemType } from '../types/item'

let items: ItemType[] = [
  {
    id: 1,
    icon: ItemIcon1,
    count: 4,
    description: {
      header: 'Зеленый',
      text: 'Очень зеленый предмет'
    }
  },
  {
    id: 2,
    icon: ItemIcon2,
    count: 2,
    description: {
      header: 'Желтый',
      text: 'Очень зеленый предмет'
    }
  },
  {
    id: 3,
    icon: ItemIcon3,
    count: 5,
    description: {
      header: 'Синий',
      text: 'Очень синий предмет'
    }
  }
]
</script>

<template>
  <div class="wrapper">
    <div class="item-field">
      <div v-for="index in 25" :key="index" class="cell">
        <div class="item" v-if="items[index - 1]">
          <div class="item-icon-wrapper">
            <img class="item-icon" :src="items[index - 1].icon" />
          </div>
          <div class="item-counter">
            <p class="item-counter-text">{{ items[index - 1].count }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  outline: 1px solid #4d4d4d;
  border-radius: 12px;
  overflow: hidden;
  position: relative;
}
.item-field {
  display: grid;
  grid-template-columns: repeat(5, 105px);
  grid-template-rows: repeat(5, 100px);
}
.cell {
  outline: 1px solid #4d4d4d;
  background: #262626;
  z-index: 1;
}
.item {
  height: calc(100% - 1px);
  position: relative;
}
.item-icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  transition: background 0.15s;
}
.item-icon-wrapper:hover {
  cursor: pointer;
  background: #2f2f2f;
}
.item-icon {
  width: 54px;
  height: 54px;
}
.item-counter {
  display: flex;
  justify-content: center;
  width: 16px;
  height: 16px;
  outline: 1px solid #4d4d4d;
  border-radius: 6px 0px 0px 0px;
  margin-left: auto;
  background: #262626;
  position: absolute;
  bottom: 0;
  right: 0;
}
.item-counter-text {
  font-size: 10px;
  font-family: Inter;
  line-height: 17px;
}
</style>
