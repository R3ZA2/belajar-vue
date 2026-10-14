<script setup>
defineProps({
  variant: {
    type: String,
    default: 'primary',
    validator: (value) =>
      ['primary', 'secondary'].includes(value),
  },
  as: {
    type: String,
    default: 'button',
  },
  to: {
    type: [String, Object],
    default: undefined,
  },
  type: {
    type: String,
    default: 'button',
  },
  disabled: {
    type: Boolean,
    default: false,
  },
})

defineEmits(['click'])
</script>

<template>
  <component
    :is="as"
    :to="to"
    :type="as === 'button' ? type : undefined"
    :disabled="as === 'button' ? disabled : undefined"
    :class="['app-button', `btn-${variant}`]"
    @click="$emit('click', $event)"
  >
    <slot />
  </component>
</template>

<style scoped>
.app-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.8rem 1.2rem;
  border: 1px solid transparent;
  border-radius: 12px;
  font: inherit;
  font-weight: 600;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-primary {
  background: #6644ff;
  color: white;
}

.btn-primary:hover {
  background: #5533ee;
  transform: translateY(-2px);
}

.btn-secondary {
  background: white;
  color: #1c1948;
  border-color: #e0e0e0;
}

.btn-secondary:hover {
  color: #6644ff;
  border-color: #6644ff;
}

.app-button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}
</style>
