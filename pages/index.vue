<template>
  <div class="">
    <h1>Events</h1>
    <event-card v-for="(event, index) in events" :key="index" :event="event" />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '../components/EventCard.vue'

export default {
  components: { EventCard },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
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
  computed: mapState({
    events: (state) => state.events.events,
  }),
}
</script>

<style></style>
