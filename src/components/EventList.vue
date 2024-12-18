<template>
  <template v-if="error">
    <SectionCard>
      <div class="flex flex-col items-center space-y-4">
        <div class="text-red-500">Could not load events at the moment. Please try again later.</div>
        <RoundButton @click="fetchEvents">Retry Now</RoundButton>
      </div>
    </SectionCard>
  </template>
  <template v-else>
    <section class="grid grid-cols-1 gap-8 lg:grid-cols-2">
      <template v-if="!loading">
        <template v-if="events.length">
          <EventCard
            v-for="event in events"
            :key="event.id"
            :title="event.title"
            :when="event.date"
            :description="event.description"
            @register="$emit('register', event)"
          />
        </template>

        <template v-else>
          <div class="col-span-2 text-center text-gray-500">No events yet.</div>
        </template>
      </template>

      <template v-else>
        <LoadingEventCard v-for="i in 4" :key="i" />
      </template>
    </section>
  </template>
</template>

<script setup>
import EventCard from '@/components/EventCard.vue';
import LoadingEventCard from '@/components/LoadingEventCard.vue';
import { ref, onMounted } from 'vue';
import SectionCard from '@/components/SectionCard.vue';
import RoundButton from './RoundButton.vue';

defineEmits(['register']);

const events = ref([]);
const loading = ref(false);
const error = ref(null);

const fetchEvents = async () => {
  loading.value = true;
  error.value = null;
  try {
    const response = await fetch('http://localhost:3001/events');
    events.value = await response.json();
  } catch (e) {
    error.value = e;
  } finally {
    loading.value = false;
  }
};

onMounted(() => {
  fetchEvents();
});
</script>
