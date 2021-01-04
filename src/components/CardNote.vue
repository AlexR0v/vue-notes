<template>
  <v-row
      justify='center'
      class='ma-4'
  >
<!--    <h2 v-if='notes.length === 0'>Add Notes</h2>-->
    <v-card
        :width='block === "block"? "350px": "100%"'
        class='ma-4'
        elevation='2'
        v-for='(note, index) in notes'
        :key='index'
    >
      <v-row justify='end'>
        <v-icon @click='deleteNote(index)'>
          mdi-close
        </v-icon>
      </v-row>
      <v-card-title>
        {{ note.title }}
      </v-card-title>
      <v-card-text>
        {{ note.description }}
        <v-row>
          <p class='ma-4'>{{ note.date }}</p>
        </v-row>
      </v-card-text>
    </v-card>
  </v-row>
</template>

<script lang='ts'>
import Vue from 'vue'

export default Vue.extend({
  name: 'CardNote',
  props: ['notes', 'block'],
  methods: {
    deleteNote(index: number) {
      this.notes.splice(index, 1)
    }
  }
})
</script>
