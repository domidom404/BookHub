<script setup lang="ts">
import { computed } from 'vue';

interface AlertDescriptionProps {
  class?: string;
}

const props = defineProps<AlertDescriptionProps>();

const descriptionClasses = computed(() => {
  return `text-muted-foreground col-start-2 grid justify-items-start gap-1 text-sm ${props.class || ''}`;
});
</script>

<template>
  <div
    :class="descriptionClasses"
    data-slot="alert-description"
  >
    <slot />
  </div>
</template>

<style scoped>
.text-muted-foreground {
  color: #6b7280;
}

:deep(p) {
  line-height: 1.625;
}
</style>