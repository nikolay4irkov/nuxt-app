<template>
  <div class="">
    <h1>{{ event.title }}</h1>
    <h3>{{ event.description }}</h3>
    <h3>{{ event.time }}</h3>
  </div>
</template>

<script>
import EventService from '@/services/EventService.js'
export default {
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await EventService.getEvent(params.id)
      return { event: data }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event' + params.id,
      })
    }
  },
}
</script>

<style></style>
