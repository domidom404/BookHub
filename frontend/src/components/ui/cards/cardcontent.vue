<script setup lang="ts">
import { computed } from 'vue';

interface CardContentProps {
  class?: string;
}

const props = defineProps<CardContentProps>();

const contentClasses = computed(() => {
  return `px-6 ${props.class || ''}`;
});
</script>

<template>
  <div :class="contentClasses" data-slot="card-content">
    <slot />
  </div>
</template>

<style scoped>
[data-slot="card-content"]:last-child {
  padding-bottom: 1.5rem;
}
</style>