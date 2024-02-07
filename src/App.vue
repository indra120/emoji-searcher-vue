<template>
  <Header />

  <main>
    <input v-model="search" type="text" placeholder="Search" />

    <Empty v-if="isLoading" text="Loading..." />
    <Empty v-if="isError" text="Error!" />

    <EmojiLists
      v-if="emojiList.length > 0"
      :emojis="emojiList"
      :search="search"
    />
  </main>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue"
import Header from "@/components/Header.vue"
import EmojiLists from "@/components/EmojiLists.vue"
import Empty from "@/components/Empty.vue"
import type { Emoji } from "@/types"

const API_URL = "https://run.mocky.io/v3/5a982f64-218d-45d7-a380-ebe924d55631"
const emojiList = ref<Emoji[]>([])
const search = ref<string>("")
const isLoading = ref<boolean>(false)
const isError = ref<boolean>(false)

onMounted(async () => {
  try {
    isLoading.value = true

    const savedList = JSON.parse(localStorage.getItem("emoji-list")!) || []
    if (savedList.length > 0) {
      emojiList.value = savedList
      return
    }

    const res = await fetch(API_URL)
    const resJson: Emoji[] = await res.json()

    emojiList.value = resJson
    localStorage.setItem("emoji-list", JSON.stringify(resJson))
  } catch (error) {
    console.error(error)
    isError.value = true
  } finally {
    isLoading.value = false
  }
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

input {
  box-shadow: var(--main-box-shadow);
  border: none;
  border-radius: 6px;
  padding: 10px;
  color: var(--main-font-color);
  font-size: 16px;
  font-weight: 600;
}
</style>
