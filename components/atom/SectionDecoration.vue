ts
<script setup lang="ts">
import { computed, defineProps, onMounted, onUnmounted, ref, withDefaults } from 'vue';

const props = withDefaults(
  defineProps<{
    direction?: 'left' | 'right';
  }>(),
  {
    direction: 'left',
  }
);

const currentImage = ref(0); // 0 or 1

const toggleImage = () => {
  currentImage.value = (currentImage.value + 1) % 2;
};

let intervalId: ReturnType<typeof setInterval>;

onMounted(() => {
  intervalId = setInterval(toggleImage, 1000); // 每秒切換一次
});

onUnmounted(() => {
  clearInterval(intervalId);
});

const desktopImageSrc = computed(() => {
  return currentImage.value === 0 ? '/images/section-decoration.svg' : '/images/section-decoration-2.svg';
});

const mobileImageSrc = computed(() => {
  return currentImage.value === 0 ? '/images/section-decoration-mobile.svg' : '/images/section-decoration-mobile-2.svg';
});

</script>

<template>
  <div
    class="p-4 overflow-hidden flex"
    :class="props.direction === 'right' ? 'justify-end' : 'justify-start'"
  >
    <!-- desktop -->
    <img
      :src="desktopImageSrc"
      class="lg:block hidden w-[750px]"
      :class="props.direction === 'right' ? 'transform scale-x-[-1]' : ''"
      alt=""
    />
    <!-- mobile -->
    <img
      :src="mobileImageSrc"
      class="lg:hidden block"
      :class="props.direction === 'right' ? 'transform scale-x-[-1]' : ''"
      alt=""
    />
  </div>
</template>