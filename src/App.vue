<template>
  <Header />

  <main></main>
</template>

<script setup lang="ts">
import Header from "@/components/Header.vue"
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