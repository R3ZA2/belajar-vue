<script setup>
import AppButton from '@/components/ui/AppButton.vue'

defineProps({
  event: {
    type: Object,
    required: true,
  },
})

defineEmits(['view-detail'])
</script>

<template>
  <article class="event-card">
    <div class="event-body">
      <div class="event-meta">
        <span class="event-date">{{ event.date }}</span>
        <span class="event-category">
          {{ event.category }}
        </span>
      </div>

      <h3>{{ event.title }}</h3>

      <p class="event-loc">
        📍 {{ event.location }}
      </p>

      <p class="event-desc">
        {{ event.description }}
      </p>

      <div class="card-footer">
        <AppButton
          variant="secondary"
          @click="$emit('view-detail', event.id)"
        >
          View Details →
        </AppButton>
      </div>
    </div>
  </article>
</template>

<style scoped>
.event-card {
  display: flex;
  flex-direction: column;
  height: 100%;
  background: white;
  border: 1px solid #f0f0f0;
  border-radius: 16px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.02);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.event-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
}

.event-body {
  display: flex;
  flex-direction: column;
  flex: 1;
  padding: 2rem;
}

.event-meta {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1.5rem;
}

.event-date {
  padding: 0.4rem 0.8rem;
  border-radius: 6px;
  background: rgba(102, 68, 255, 0.1);
  color: #6644ff;
  font-size: 0.85rem;
  font-weight: 600;
}

.event-category {
  color: #888;
  font-size: 0.85rem;
  font-weight: 500;
  text-transform: uppercase;
}

h3 {
  margin: 0 0 0.8rem;
  color: #1c1948;
  font-size: 1.4rem;
}

.event-loc {
  margin-bottom: 1.5rem;
  color: #666;
  font-size: 0.95rem;
}

.event-desc {
  flex: 1;
  margin-bottom: 2rem;
  color: #555;
  font-size: 0.95rem;
  line-height: 1.6;
}

.card-footer {
  padding-top: 1.5rem;
  border-top: 1px solid #f0f0f0;
}

.card-footer :deep(.app-button) {
  padding: 0;
  border: none;
  border-radius: 0;
  color: #1c1948;
}

.card-footer :deep(.app-button:hover) {
  color: #6644ff;
  background: transparent;
  transform: none;
}
</style>
