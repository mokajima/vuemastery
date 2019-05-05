<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard'

export default {
  head() {
    return {
      title: 'Event Listing'
    }
  },
  components: {
    EventCard
  },
  async asyncData({ $axios, error }) {
    try {
      const response = await $axios.get('http://localhost:3000/events')
      return {
        events: response.data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. please try again.'
      })
    }
  }
}
</script>
