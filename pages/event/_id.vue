<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about ' + this.event.title
        }
      ]
    }
  },
  async asyncData({ $axios, error, params }) {
    try {
      const response = await $axios.get(
        'http://localhost:3001/events/' + params.id
      )
      return {
        event: response.data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event #' + params.id
      })
    }
  }
}
</script>
