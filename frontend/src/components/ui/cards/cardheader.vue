<script setup lang="ts">
import { computed } from 'vue';

interface CardHeaderProps {
  class?: string;
}

const props = defineProps<CardHeaderProps>();

const headerClasses = computed(() => {
  return `grid auto-rows-min grid-rows-[auto_auto] items-start gap-1.5 px-6 pt-6 ${props.class || ''}`;
});
</script>

<template>
  <div :class="headerClasses" data-slot="card-header">
    <slot />
  </div>
</template>

<style scoped>
</style>