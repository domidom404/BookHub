<script setup lang="ts">
import { computed } from 'vue';

interface CardProps {
  class?: string;
}

const props = defineProps<CardProps>();

const cardClasses = computed(() => {
  return `bg-card text-card-foreground flex flex-col gap-6 rounded-xl border ${props.class || ''}`;
});
</script>

<template>
  <div :class="cardClasses" data-slot="card">
    <slot />
  </div>
</template>

<style scoped>
.bg-card {
  background-color: white;
}

.text-card-foreground {
  color: #111827;
}

.rounded-xl {
  border-radius: 0.75rem;
}

.border {
  border: 1px solid #e5e7eb;
}
</style>