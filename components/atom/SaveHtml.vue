<script setup lang="ts">
defineProps<{
  html: string;
}>();
</script>

<template>
  <!-- eslint-disable vue/no-v-html -->
  <div class="html-content" v-html="$sanitize(html)"></div>
</template>

<style scoped>
.html-content {
  word-break: break-word;
  overflow-wrap: anywhere;
}

.html-content :deep(a) {
  word-break: break-all;
  overflow-wrap: break-word;
  display: inline-block;
  max-width: 100%;
}
</style>
