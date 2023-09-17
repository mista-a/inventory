<script setup lang="ts">
import type { ItemType } from '@/types/item'
import CloseIcon from '@/components/icons/CloseIcon.vue'
import CustomButton from '@/components/ui/CustomButton.vue'
import CustomDivider from '@/components/ui/CustomDivider.vue'
import ModalWindow from '@/components/ModalWindow.vue'
import { ref, watch } from 'vue'

interface ItemDescriptionProps {
  choosedItem: ItemType
  active: boolean
}

interface ItemDescriptionEmits {
  (e: 'change:itemCount', id: number, count: number): void
  (e: 'close'): void
}

const props = defineProps<ItemDescriptionProps>()
const emit = defineEmits<ItemDescriptionEmits>()

const deleteMenu = ref(false)
const deleteCount = ref<number | null>(null)

const inputIntFilter = (e: Event) => {
  const target = e.target as HTMLInputElement
  const inputText = +target.value.replace(/[^0-9]/g, '')

  if (!inputText) deleteCount.value = null

  const maxCount = props.choosedItem.count
  if (inputText > maxCount) {
    deleteCount.value = maxCount
  }
}

const toggleItemDeleteMenu = () => {
  deleteMenu.value = !deleteMenu.value
}

const disableItemDeleteMenu = () => {
  deleteCount.value = null
  deleteMenu.value = false
}

const hideMenu = () => {
  emit('close')
  disableItemDeleteMenu()
}

const deleteItems = () => {
  toggleItemDeleteMenu()
  if (deleteCount.value) {
    emit('change:itemCount', props.choosedItem.id, deleteCount.value)
  }
}

watch(
  () => props.choosedItem.id,
  () => {
    disableItemDeleteMenu()
  }
)
</script>

<template>
  <ModalWindow :active="active" :position="'right'" :animation-duration="1.2">
    <div class="item-descrption">
      <CustomButton class="close" @click="hideMenu">
        <CloseIcon />
      </CustomButton>
      <img class="item-img" :src="choosedItem.icon" alt="item" />
      <CustomDivider class="divider top-divider" />
      <h2>{{ choosedItem.description.header }} x {{ choosedItem.count }}</h2>
      <p class="description-text">{{ choosedItem.description.text }}</p>
      <CustomDivider class="divider bottom-divider" />
      <div class="delete">
        <div class="delete-menu" v-if="deleteMenu">
          <input
            class="delete-count"
            placeholder="Введите количество"
            v-model="deleteCount"
            @input="inputIntFilter($event)"
          />
          <div class="delete-buttons">
            <CustomButton class="delete-menu-cancel-button" @click="toggleItemDeleteMenu">
              Отмена
            </CustomButton>
            <CustomButton class="delete-menu-accept-button" @click="deleteItems">
              Подтвердить
            </CustomButton>
          </div>
        </div>
        <CustomButton class="delete-button" @click="toggleItemDeleteMenu" v-else>
          Удалить предмет
        </CustomButton>
      </div>
    </div>
  </ModalWindow>
</template>

<style scoped>
.item-descrption {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(38, 38, 38, 0.5);
  backdrop-filter: blur(8px);
  padding: 8px 15px 18px;
  width: 250px;
  height: 100%;
  border-left: 1px solid #4d4d4d;
}

.close {
  margin-left: auto;
  width: 24px;
  height: 24px;
  margin-bottom: 23px;
}

.item-img {
  width: 130px;
  height: 130px;
  margin-bottom: 30px;
}

.divider {
  background: #4d4d4d;
}

.top-divider {
  margin-bottom: 16px;
}

.description-text {
  flex: 1;
  overflow-y: auto;
}

.delete {
  width: 100%;
  margin-top: 18px;
  font-family: SF Pro Display;
}

.delete-button {
  transition: background 0.3s;
  height: 39px;
  color: white;
  background: #fa7272;
  border-radius: 8px;
}

.delete-button:hover {
  background: #f88;
}

.delete-menu {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.delete-count {
  border-radius: 4px;
  border: 1px solid #4d4d4d;
  background: #262626;
  color: #fff;
  height: 40px;
  padding: 12px 0px 12px 12px;
}

.delete-buttons {
  display: flex;
  gap: 10px;
  height: 33px;
}

.delete-menu-cancel-button {
  width: 88px;
  padding: 0 28px;
  border-radius: 8px;
  color: #2d2d2d;
  background: #fff;
}

.delete-menu-accept-button {
  border-radius: 8px;
  background: #fa7272;
  color: #fff;
}
</style>
