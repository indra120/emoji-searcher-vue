<template>
  <div class="emoji-lists">
    <EmojiBox
      v-for="({ title, symbol }, i) in emojis.splice(0, 20)"
      :key="i"
      :title="title"
      :symbol="symbol"
    />
  </div>
</template>

<script setup lang="ts">
import EmojiBox from "./EmojiBox.vue"
import type { Emoji } from "@/types"

defineProps<{ emojis: Emoji[] }>()
</script>

<style scoped>
.emoji-lists {
  display: flex;
  flex-flow: row wrap;
  justify-content: flex-start;
  margin-top: 32px;
}
</style>
