<script setup>
defineProps({
  categories: {
    type: Array,
    default: () => ['All'],
  },
  modelValue: {
    type: String,
    default: 'All',
  },
})

defineEmits(['update:modelValue'])
</script>

<template>
  <div class="category-filter" aria-label="Filter event category">
    <button
      v-for="category in categories"
      :key="category"
      type="button"
      :class="{ active: modelValue === category }"
      :aria-pressed="modelValue === category"
      @click="$emit('update:modelValue', category)"
    >
      {{ category }}
    </button>
  </div>
</template>

<style scoped>
.category-filter {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

button {
  padding: 0.65rem 1.1rem;
  border: 1px solid #e0e0e0;
  border-radius: 999px;
  background: white;
  color: #555;
  font: inherit;
  font-size: 0.9rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

button:hover {
  border-color: #6644ff;
  color: #6644ff;
}

button.active {
  border-color: #6644ff;
  background: #6644ff;
  color: white;
}
</style>
