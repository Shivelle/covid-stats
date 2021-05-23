<template>
  <div class="text-center">
    <h2 class="text-3xl font-semibold">{{ text }}
    </h2>
    <div class="mt-5 mb-8 text-gray-700">
      <span class="font-semibold">Last Update: </span>{{ timestamp }}
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'DataTitle',
  props: ['text', 'dataDate'],
  computed: {
    timestamp: function() {
      return moment(this.dataDate).format('📆DD.MM.YYYY ⌚h:mm:ss')
    }
  }
}
</script>