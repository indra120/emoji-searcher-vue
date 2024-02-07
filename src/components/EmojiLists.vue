<template>
  <div class="emoji-lists">
    <EmojiBox
      v-for="({ title, symbol }, i) in filteredEmojis"
      :key="i"
      :title="title"
      :symbol="symbol"
    />
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, watch } from "vue"
import EmojiBox from "./EmojiBox.vue"
import type { Emoji } from "@/types"
import { SearchEmojiParams, searchEmoji } from "@/utils/searchEmoji"

const props = defineProps<Omit<SearchEmojiParams, "maxResults">>()
const filteredEmojis = ref<Emoji[]>([])

const filter = () => {
  filteredEmojis.value = searchEmoji(props)
}

onMounted(filter)
watch(props, filter)
</script>

<style scoped>
.emoji-lists {
  display: flex;
  flex-flow: row wrap;
  justify-content: flex-start;
  margin-top: 32px;
}
</style>
