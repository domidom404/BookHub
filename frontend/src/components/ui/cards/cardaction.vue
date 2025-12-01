<script setup lang="ts">
import { computed } from 'vue';

interface CardActionProps {
  class?: string;
}

const props = defineProps<CardActionProps>();

const actionClasses = computed(() => {
  return `col-start-2 row-span-2 row-start-1 self-start justify-self-end ${props.class || ''}`;
});
</script>

<template>
  <div :class="actionClasses" data-slot="card-action">
    <slot />
  </div>
</template>

<style scoped>
</style>