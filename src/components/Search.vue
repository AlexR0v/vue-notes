<template>
  <div style='max-width: 250px'>
    <v-text-field
        class='mt-4'
        label='Search note'
        filled
        prepend-inner-icon='mdi-magnify'
        rounded
        dense
        v-model='search'
    ></v-text-field>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue'

export default Vue.extend({
  name: 'Search',
  props: {
    value: {
      type: String,
      required: true
    }
  },
  data(){
    return{
      search: this.value
    }
  },
  watch:{
    search(val){
      this.$emit('search', val)
    }
  }

})
</script>
