<script setup>
import EventCard from '@/components/EventCard.vue'
import axios from 'axios'
import { ref, onMounted } from 'vue'

const events = ref(null)

onMounted(async () => {
  try {
    const response = await axios.get(
      'http://my-json-server.typicode.com/Code-Pop/Real-World_Vue-3/events'
    )
    events.value = response.data
  } catch (error) {
    console.error('Error fetching events:', error)
  }
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
