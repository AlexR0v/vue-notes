<template>
  <v-alert
      max-width='350px'
      type='error'
  >
    Title or description can`t be blank!
  </v-alert>
</template>

<script lang='ts'>
import Vue from 'vue'
export default Vue.extend({
  name: 'Alert'
})
</script>
