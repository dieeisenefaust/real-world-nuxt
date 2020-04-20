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
import { mapState } from 'vuex'
import EventCard from '~/components/EventCard.vue'
// import EventService from '~/services/EventService.js'

export default {
  components: {
    EventCard
  },
  async fetch({ store, error }) {
    // async asyncData({ error }) {
    // return $axios
    //   .get('http://localhost:3000/events')
    //   .then((response) => {
    //     return {
    //       events: response.data
    //     }
    //   })
    try {
      // const { data } = await $axios.get('http://localhost:3000/events')

      // const { data } = await EventService.getEvents()
      // return {
      //   events: data
      // }
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again.'
      })
    }
  },
  computed: mapState({
    events: (state) => state.events.events
  }),
  head() {
    return {
      title: 'Event Listing'
    }
  }
}
</script>
