<script setup>
defineProps({
  modelValue: {
    type: String,
    default: '',
  },
})

defineEmits(['update:modelValue'])
</script>

<template>
  <div class="search-bar">
    <span class="search-icon" aria-hidden="true">⌕</span>

    <input
      type="search"
      :value="modelValue"
      placeholder="Search events..."
      aria-label="Search events"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>

<style scoped>
.search-bar {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  width: 100%;
  box-sizing: border-box;
  padding: 0 1rem;
  border: 1px solid #e5e5e5;
  border-radius: 12px;
  background: white;
}

.search-icon {
  color: #777;
  font-size: 1.5rem;
}

input {
  width: 100%;
  min-width: 0;
  padding: 1rem 0;
  border: none;
  outline: none;
  background: transparent;
  color: #1c1948;
  font: inherit;
}

.search-bar:focus-within {
  border-color: #6644ff;
  box-shadow: 0 0 0 3px rgba(102, 68, 255, 0.08);
}
</style>
