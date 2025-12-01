<script setup lang="ts">
import { computed } from 'vue';

interface CardDescriptionProps {
  class?: string;
}

const props = defineProps<CardDescriptionProps>();

const descClasses = computed(() => {
  return `text-muted-foreground text-sm ${props.class || ''}`;
});
</script>

<template>
  <p :class="descClasses" data-slot="card-description">
    <slot />
  </p>
</template>

<style scoped>
.text-muted-foreground {
  color: #6b7280;
}
</style>