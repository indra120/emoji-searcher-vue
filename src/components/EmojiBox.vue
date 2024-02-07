<template>
  <div @click="copyToClipboard" class="emoji-box" :class="{ 'selected' : isSelected }">
    <p class="emoji" v-html="`&#${symbol.codePointAt(0)};`"></p>
    <p class="emoji-text" :class="{ 'selected-text' : isSelected }">
      {{ isSelected ? "Copied!" : title }}
    </p>
  </div>
</template>

<script setup lang="ts">
import { onUnmounted, onUpdated, ref } from "vue"
import { Emoji } from "@/types"

const props = defineProps<Omit<Emoji, "keywords">>()
const isSelected = ref<boolean>(false)
const timer = ref<NodeJS.Timeout>()

onUpdated(() => {
  timer.value = setTimeout(() => (isSelected.value = false),600)
})

onUnmounted(() => {
  clearTimeout(timer.value)
})

const copyToClipboard = () => {
  navigator.clipboard.writeText(props.symbol)
  isSelected.value = true
}
</script>

<style scoped>
.emoji-box {
  background-color: var(--secondary-background-color);
  box-shadow: var(--main-box-shadow);
  border-radius: 4px;
  padding: 8px;
  margin: 4px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  flex: 1;
  min-height: 100px;
  min-width: 100px;
  transition: all 0.4s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

.selected {
  transform: rotate(32deg) scale(1.4, 1.4);
  box-shadow: var(--main-box-shadow-elevated);
}

.emoji {
  font-size: 40px;
}

.emoji-text {
  font-size: 12px;
  font-weight: 600;
}

.selected-text {
  font-size: 16px;
  font-weight: bold;
}
</style>