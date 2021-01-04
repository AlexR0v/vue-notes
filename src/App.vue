<template>
  <v-app>
    <v-container
        tag='section'
        class='grey lighten-5'
    >
      <v-col align='center'>
        <h1>{{ title }}</h1>
        <Inputs
            :notes='notes'
        />
        <v-col
            sm='5'
            align='start'
            justify='center'
        >
          <v-row
              class='ma-4'
              justify='space-between'
          >
            <Search
                :value='search'
                @search='search = $event'
            />
            <div
                class='icon_wrapper'
            >
              <v-icon
                  class='list_icon'
                  style='cursor: pointer'
                  @click='block = "list"'
              >
                mdi-format-list-bulleted
              </v-icon>
              <v-icon
                  class='list_icon'
                  style='cursor: pointer'
                  @click='block = "block"'
              >
                mdi-view-grid-outline
              </v-icon>
            </div>
          </v-row>
        </v-col>
        <CardNote
            :block='block'
            :notes='notesFilter'
        />
      </v-col>
    </v-container>
  </v-app>
</template>

<script lang='ts'>
import Vue from 'vue'
import Inputs from '@/components/Inputs.vue'
import CardNote from '@/components/CardNote.vue'
import Search from '@/components/Search.vue'

export default Vue.extend({
  name: 'App',
  components: {
    Inputs,
    CardNote,
    Search
  },
  data() {
    return {
      title: 'Notes App',
      block: 'block',
      search: '',
      notes: <Array<object>>[
        {title: 'First Note', description: 'Description for first note', date: new Date().toLocaleString()},
        {title: 'Second Note', description: 'Description for second note', date: new Date().toLocaleString()},
        {title: 'Third Note', description: 'Description for first note', date: new Date().toLocaleString()}
      ]
    }
  },
  computed: {
    notesFilter() {
      let arr: any = this.notes
      let search = this.search
      if (!search) return arr
      search = search.trim().toLowerCase()
      arr = arr.filter((item: any) => {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      return arr
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

.icon_wrapper {
  display: flex;
  width: 70px;
  justify-content: space-between;
  align-items: center;
}
</style>
