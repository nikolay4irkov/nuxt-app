<template>
  <div class="">
    <h1>Events</h1>
    <event-card v-for="(event, index) in events" :key="index" :event="event" />
  </div>
</template>

<script>
import EventService from '@/services/EventService.js'
import EventCard from '../components/EventCard.vue'

export default {
  components: { EventCard },
  async asyncData({ error }) {
    try {
      const { data } = await EventService.getEvents()
      return { events: data }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event now',
      })
    }
  },
  head() {
    return {
      title: 'Event Listing - Real World Events',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Where you can find',
        },
      ],
    }
  },
}
</script>

<style></style>
