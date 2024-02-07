<template>
  <header>
    <img :src="emojiIcon" alt="emoji icon" />
    <img :src="searchIcon" alt="search icon" />
    <span> EmojiSearch </span>
  </header>
</template>

<script setup lang="ts">
import searchIcon from "@/assets/search-icon.svg"
import emojiIcon from "@/assets/emoji-icon.svg"
</script>

<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: var(--main-background-color);
  padding: 0 16px;
  height: 55px;
}

span {
  color: var(--secondary-font-color);
  font-size: 24px;
  font-weight: bold;
}

img {
  height: 32px;
  width: 32px;
}

img:nth-child(1) {
  margin-right: 8px;
}

img:nth-child(2) {
  margin-top: 3px;
}
</style>
