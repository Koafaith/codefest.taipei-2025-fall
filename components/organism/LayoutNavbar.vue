<script setup lang="ts">
import { ROUTE_PATHS } from '~/constants/routes';

const props = defineProps<{
  type: 'header' | 'mobile-header' | 'footer';
  navClass: string;
}>();

const dialogStore = useDialogStore();

const { tm } = useI18n();

// 計算不同類型的 nav-item class
const navItemClass = computed(() => {
  const typeMap: Record<string, string> = {
    header: 'header-nav-item',
    'mobile-header': 'mobile-header-nav-item',
    footer: 'footer-nav-item',
  };
  return typeMap[props.type] || '';
});
</script>

<template>
  <nav>
    <ul :class="navClass">
      <li :class="navItemClass">
        <NuxtLink
          v-kb-focus="{
            id: `${type}-nav2-${type === 'header' ? 1 : 202}`,
            x: 2,
            y: type === 'header' ? 1 : 202,
          }"
          :to="ROUTE_PATHS.RULES"
          @click="dialogStore.closeDialog()"
          >競賽規則</NuxtLink
        >
      </li>
      <li :class="navItemClass">
        <NuxtLink
          v-kb-focus="{
            id: `${type}-nav3-${type === 'header' ? 1 : 202}`,
            x: 3,
            y: type === 'header' ? 1 : 202,
          }"
          :to="`${ROUTE_PATHS.RULES}${ROUTE_PATHS.SCHEDULE}`"
          @click="dialogStore.closeDialog()"
          >重要時程</NuxtLink
        >
      </li>
      <li :class="navItemClass">
        <NuxtLink
          v-kb-focus="{
            id: `${type}-nav4-${type === 'header' ? 1 : 202}`,
            x: 4,
            y: type === 'header' ? 1 : 202,
          }"
          :to="`${ROUTE_PATHS.RULES}${ROUTE_PATHS.FAQ}`"
          @click="dialogStore.closeDialog()"
          >FAQ</NuxtLink
        >
      </li>
      <li :class="navItemClass">
        <NuxtLink
          v-kb-focus="{
            id: `${type}-nav5-${type === 'header' ? 1 : 202}`,
            x: 5,
            y: type === 'header' ? 1 : 202,
          }"
          :to="ROUTE_PATHS.PAST"
          @click="dialogStore.closeDialog()"
          >參賽回顧</NuxtLink
        >
      </li>
      <li :class="navItemClass">
        <a
          v-kb-focus="{
            id: `${type}-nav6-${type === 'header' ? 1 : 202}`,
            x: 6,
            y: type === 'header' ? 1 : 202,
          }"
          :href="tm('past_url')"
          target="_blank"
          @click="dialogStore.closeDialog()"
          >歷屆紀錄</a
        >
      </li>
    </ul>
  </nav>
</template>

<style scoped lang="postcss">
.header-nav-item {
  @apply px-4;
}

.footer-nav-item {
  @apply pr-4 py-2;
}

.mobile-header-nav-item {
  @apply p-8 border-b border-b-white last:border-b-0;
}
</style>
