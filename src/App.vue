<template>
  <v-app>
    <v-container
        tag='section'
        class='grey lighten-5'
    >
      <v-col align='center'>
        <h1>{{ title }}</h1>
        <v-col sm='5'>
          <v-row
              align='center'
              class='mb-4'
          >
            <v-text-field
                class='ma-4'
                label='Title'
                v-model='newNoteTitle'
            ></v-text-field>
            <v-text-field
                label='Description'
                v-model='newNoteDescription'
            ></v-text-field>
          </v-row>
          <v-alert
              max-width='350px'
              type='error'
              v-if='error'
          >
            Title or description can`t be blank!
          </v-alert>
          <v-btn
              color='info'
              @click='addNewNote'
          >New note
          </v-btn>
        </v-col>
        <v-col
            sm='5'
            align='start'
            justify='center'
        >
          <div style='max-width: 250px'>
            <v-text-field
                label='Search note'
                filled
                prepend-inner-icon='mdi-magnify'
                rounded
                dense
            ></v-text-field>
          </div>
        </v-col>
        <v-row
            justify='center'
            class='ma-4'
        >
          <h2 v-if='notes.length === 0'>Add Notes</h2>
          <v-card
              width='350px'
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
      </v-col>
    </v-container>
  </v-app>
</template>

<script lang='ts'>
import Vue from 'vue'

export default Vue.extend({
  name: 'App',
  components: {},
  data() {
    return {
      title: 'Notes App',
      newNoteTitle: '',
      newNoteDescription: '',
      error: false,
      notes: [
        {title: 'First Note', description: 'Description for first note', date: new Date().toLocaleString()},
        {title: 'Second Note', description: 'Description for second note', date: new Date().toLocaleString()},
        {title: 'Third Note', description: 'Description for first note', date: new Date().toLocaleString()}
      ]
    }
  },
  methods: {
    addNewNote() {
      if (this.newNoteTitle && this.newNoteDescription) {
        const newNote = {
          title: this.newNoteTitle,
          description: this.newNoteDescription,
          date: new Date().toLocaleString()
        }
        this.notes.unshift(newNote)
        this.newNoteTitle = ''
        this.newNoteDescription = ''
      } else {
        this.error = true
        setTimeout(() => {
          this.error = false
        }, 2000)
      }
    },
    deleteNote(index) {
      this.notes.splice(index, 1)
    }
  }
})
</script>

<style>
body {
  font-family: 'Montserrat', sans-serif;
  color: #2c3e50;
}

.container {
  height: 100ch;
}

.v-card__title {
  text-transform: capitalize;
}

.row .justify-end i {
  cursor: pointer;
}
</style>
