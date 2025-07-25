<script setup>
import { ref } from 'vue'
import EventService from '../services/EventService'
import { onMounted } from 'vue'

const event = ref(null)

const props = defineProps({
  id: {
    type: Number,
    required: true,
  },
})

onMounted(async () => {
  // fetch event (by id) and set local data.
  try {
    const response = await EventService.getEvent(props.id)
    event.value = response.data
  } catch (error) {
    console.log('error fetching event:', error)
  }
})
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>
