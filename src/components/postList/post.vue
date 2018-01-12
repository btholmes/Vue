<template>
  <md-card class="post">
    <md-card-header>
      <div class="md-title">
        {{ title }} <small>{{ when }}</small>
      </div>
      <div class="md-subhead">{{ author }}</div>
    </md-card-header>

    <md-card-content v-if="description">
      {{ description }}
    </md-card-content>

    <md-card-expand>
      <md-card-actions>
        <md-button class="md-raised md-primary">
          <md-icon>check</md-icon> Attend
        </md-button>
        <md-button class="md-raised">
          <md-icon>clear</md-icon> No Thanks
        </md-button>
        <span style="flex: 1"></span>
        <md-icon v-if="location">pin_drop</md-icon>
        <md-button v-if="location" class="md-icon-button" md-expand-trigger>
          <md-icon>keyboard_arrow_down</md-icon>
        </md-button>
      </md-card-actions>

      <md-card-content v-if="location">
        This will be a map
      </md-card-content>
    </md-card-expand>
  </md-card>
</template>

<script>
export default {
  name: 'post',
  props: {
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      default: ''
    },
    datetime: {
      type: Number,
      required: true
    },
    location: {
      type: String
    },
    author: {
      type: String,
      required: true
    },
    timestamp: {
      type: Number,
      required: true
    }
  },
  data () {
    return {
    }
  },
  computed: {
    when () {
      let currentDate = new Date()
      let eventDate = new Date(this.datetime)
      return (
        (eventDate.getDate() === currentDate.getDate() ? 'Today' : 'Tomorrow') +
        ' at ' +
        (eventDate.getHours() % 12 || 12) +
        ':' +
        eventDate.getMinutes() +
        ' ' +
        (eventDate.getHours() < 12 ? 'AM' : 'PM')
      )
    }
  }
}
</script>

<style>
.post {
  flex: 1 100%;
  margin: 1em;
}
</style>
