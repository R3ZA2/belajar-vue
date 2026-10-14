<script setup>
import { computed, ref } from 'vue'
import { useRouter } from 'vue-router'

import EventCard from '@/components/event/EventCard.vue'
import SearchBar from '@/components/event/SearchBar.vue'
import CategoryFilter from '@/components/event/CategoryFilter.vue'

const router = useRouter()

const searchQuery = ref('')
const selectedCategory = ref('All')

const events = ref(
  Array.from({ length: 6 }, (_, index) => {
    const id = index + 1

    return {
      id,
      title: `Community Gathering ${id}`,
      date: `Oct ${10 + id}, 2026`,
      category: 'Community',
      location: 'Main Auditorium, City Center',
      description:
        'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam at velit vel magna interdum scelerisque.',
    }
  }),
)

const categories = computed(() => [
  'All',
  ...new Set(events.value.map((event) => event.category)),
])

const filteredEvents = computed(() => {
  const keyword = searchQuery.value.trim().toLowerCase()

  return events.value.filter((event) => {
    const matchesSearch = [
      event.title,
      event.location,
      event.description,
      event.category,
    ].some((value) => value.toLowerCase().includes(keyword))

    const matchesCategory =
      selectedCategory.value === 'All' ||
      event.category === selectedCategory.value

    return matchesSearch && matchesCategory
  })
})

function viewDetail(id) {
  router.push({
    name: 'event-detail',
    params: { id },
  })
}
</script>

<template>
  <div class="event-list-page">
    <div class="header-section">
      <h2 class="section-title">Upcoming Events</h2>
      <p class="section-desc">
        Discover the latest gatherings and activities happening near you.
      </p>
    </div>

    <div class="event-controls">
      <SearchBar v-model="searchQuery" />

      <CategoryFilter
        v-model="selectedCategory"
        :categories="categories"
      />
    </div>

    <p class="result-count" aria-live="polite">
      {{ filteredEvents.length }}
      {{ filteredEvents.length === 1 ? 'event' : 'events' }} found
    </p>

    <div v-if="filteredEvents.length" class="event-grid">
      <EventCard
        v-for="event in filteredEvents"
        :key="event.id"
        :event="event"
        @view-detail="viewDetail"
      />
    </div>

    <div v-else class="empty-state">
      <div class="empty-icon">🔎</div>
      <h3>No events found</h3>
      <p>
        Try another keyword or choose a different category.
      </p>

      <button
        type="button"
        class="reset-button"
        @click="
          searchQuery = ''
          selectedCategory = 'All'
        "
      >
        Reset Search
      </button>
    </div>
  </div>
</template>

<style scoped>
.event-list-page {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.header-section {
  margin-bottom: 1rem;
}

.section-title {
  margin-bottom: 0.5rem;
  color: #1c1948;
  font-size: 2.2rem;
}

.section-desc {
  color: #666;
  font-size: 1.1rem;
  line-height: 1.6;
}

.event-controls {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.result-count {
  margin: 0;
  color: #777;
  font-size: 0.9rem;
}

.event-grid {
  display: grid;
  grid-template-columns: repeat(
    auto-fill,
    minmax(min(100%, 320px), 1fr)
  );
  align-items: stretch;
  gap: 2rem;
}

.empty-state {
  padding: 4rem 1rem;
  text-align: center;
  border: 1px dashed #ddd;
  border-radius: 16px;
  background: #fafafa;
}

.empty-icon {
  margin-bottom: 1rem;
  font-size: 2.5rem;
}

.empty-state h3 {
  margin-bottom: 0.75rem;
  color: #1c1948;
}

.empty-state p {
  color: #666;
}

.reset-button {
  margin-top: 1rem;
  padding: 0.75rem 1.25rem;
  border: none;
  border-radius: 10px;
  background: #6644ff;
  color: white;
  font: inherit;
  font-weight: 600;
  cursor: pointer;
}

.reset-button:hover {
  background: #5533ee;
}

@media (max-width: 480px) {
  .section-title {
    font-size: 1.8rem;
  }

  .event-grid {
    grid-template-columns: 1fr;
  }
}
</style>
