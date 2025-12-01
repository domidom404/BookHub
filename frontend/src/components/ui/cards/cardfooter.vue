<script setup lang="ts">
import { computed } from 'vue';

interface CardFooterProps {
  class?: string;
}

const props = defineProps<CardFooterProps>();

const footerClasses = computed(() => {
  return `flex items-center px-6 pb-6 ${props.class || ''}`;
});
</script>

<template>
  <div :class="footerClasses" data-slot="card-footer">
    <slot />
  </div>
</template>

<style scoped>
.border-t {
  border-top: 1px solid #e5e7eb;
  padding-top: 1.5rem;
}
</style>