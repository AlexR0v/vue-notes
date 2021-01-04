<template>
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
    <Alert v-if='error'/>
    <v-btn
        color='info'
        @click='addNewNote'
    >Add note
    </v-btn>
  </v-col>
</template>

<script lang='ts'>
import Vue from 'vue'
import Alert from '@/components/Alert.vue'

export default Vue.extend({
  name: 'Inputs',
  components: {
    Alert
  },
  props: {
    notes: {
      type: Array,
      required: true
    }
  },
  data(){
    return{
      newNoteTitle: '',
      newNoteDescription: '',
      error: false
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
  }
})
</script>
