<template>
  <Header />

  <main>
    <EmojiLists v-if="emojiList.length > 0" :emojis="emojiList" />
  </main>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue"
import Header from "@/components/Header.vue"
import type { Emoji } from "@/types"
import EmojiLists from "./components/EmojiLists.vue"

const API_URL = "https://run.mocky.io/v3/5a982f64-218d-45d7-a380-ebe924d55631"
const emojiList = ref<Emoji[]>([])

onMounted(async () => {
  const savedList = JSON.parse(localStorage.getItem("emoji-list")!) || []
  if (savedList.length > 0) {
    emojiList.value = savedList
  } else {
    const res = await fetch(API_URL)
    const resJson: Emoji[] = await res.json()
    emojiList.value = resJson
    localStorage.setItem("emoji-list", JSON.stringify(resJson))
  }

  console.log(emojiList.value)
})
</script>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  min-height: calc(100vh - 55px);
  max-width: 480px;
  padding: 16px;
  margin: 0 auto;
  background-color: var(--main-container-color);
}
</style>
