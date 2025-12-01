<script setup lang="ts">
import { computed } from 'vue';

interface MenubarProps {
  class?: string;
}

const props = defineProps<MenubarProps>();

const menubarClasses = computed(() => {
  return `bg-background flex h-9 items-center gap-1 rounded-md border p-1 shadow-xs ${props.class || ''}`;
});
</script>

<template>
  <div :class="menubarClasses" data-slot="menubar" role="menubar">
    <slot />
  </div>
</template>

<style scoped>
.shadow-xs {
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}
</style>