<script setup lang="ts">
import { computed } from 'vue';

interface CardTitleProps {
  class?: string;
}

const props = defineProps<CardTitleProps>();

const titleClasses = computed(() => {
  return `leading-none font-semibold text-lg ${props.class || ''}`;
});
</script>

<template>
  <h4 :class="titleClasses" data-slot="card-title">
    <slot />
  </h4>
</template>

<style scoped>
</style>