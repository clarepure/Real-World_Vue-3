<template>
  <div class="events">
    <h1>Events For Good</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
// @ is an alias to /src
import EventService from '@/services/EventService'
import EventCard from '@/components/EventCard.vue'

export default {
  name: 'EventList',
  components: {
    EventCard,
  },
  data() {
    return {
      events: null
    }
  },
  created() {
    //get events from mock db when component is created
    EventService.getEvents()
      .then(response => {
        this.events = response.data
      })
      .catch(error => console.log(error))
  }
}
    /* old inefficient
    axios.get('https://my-json-server.typicode.com/clarepure/Real-World_Vue-3/events').then(response => {
      this.events = response.data
    })
    .catch(error => {
      console.log(error)
    })
    */
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
