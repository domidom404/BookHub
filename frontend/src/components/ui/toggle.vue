<script setup lang="ts">
import { ref, computed } from 'vue';

interface ToggleProps {
  variant?: 'default' | 'outline';
  size?: 'default' | 'sm' | 'lg';
  modelValue?: boolean;
  disabled?: boolean;
}

const props = withDefaults(defineProps<ToggleProps>(), {
  variant: 'default',
  size: 'default',
  modelValue: false,
  disabled: false,
});

const emit = defineEmits<{
  'update:modelValue': [value: boolean];
}>();

const isPressed = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
});

const toggleState = () => {
  if (!props.disabled) {
    isPressed.value = !isPressed.value;
  }
};

const toggleClasses = computed(() => {
  const baseClasses = 'inline-flex items-center justify-center gap-2 rounded-md text-sm font-medium hover:bg-muted hover:text-muted-foreground disabled:pointer-events-none disabled:opacity-50 focus-visible:border-ring focus-visible:ring-ring/50 focus-visible:ring-[3px] outline-none transition-[color,box-shadow] aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive whitespace-nowrap';
  
  const variantClasses = {
    default: 'bg-transparent',
    outline: 'border border-input bg-transparent hover:bg-accent hover:text-accent-foreground',
  };
  
  const sizeClasses = {
    default: 'h-9 px-2 min-w-9',
    sm: 'h-8 px-1.5 min-w-8',
    lg: 'h-10 px-2.5 min-w-10',
  };
  
  const stateClasses = isPressed.value ? 'bg-accent text-accent-foreground' : '';
  
  return `${baseClasses} ${variantClasses[props.variant]} ${sizeClasses[props.size]} ${stateClasses}`;
});
</script>

<template>
  <button
    type="button"
    :class="toggleClasses"
    :disabled="disabled"
    :aria-pressed="isPressed"
    :data-state="isPressed ? 'on' : 'off'"
    data-slot="toggle"
    @click="toggleState"
  >
    <slot />
  </button>
</template>

<style scoped>
/* Toggle styles */
button[data-state="on"] {
  background-color: var(--accent);
  color: var(--accent-foreground);
}
</style>