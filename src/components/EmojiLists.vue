<template>
  <div v-if="filteredEmojis.length > 0" class="emoji-lists">
    <EmojiBox v-for="({ title, symbol }, i) in filteredEmojis" :key="i" :title="title" :symbol="symbol" />
  </div>

  <Empty v-else text="Oops, zero finding. Let's try another keyword!" />
</template>

<script setup lang="ts">
import { onMounted, ref, watch } from "vue"
import EmojiBox from "./EmojiBox.vue"
import Empty from "./Empty.vue"
import { type SearchEmojiParams, searchEmoji } from "@/utils/searchEmoji"
import type { Emoji } from "@/types"

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
