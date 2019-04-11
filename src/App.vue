<template>
  <div class="wrapper">
      <div class="wrapper-content">
        <section>
          <div class="container">
            <h1> {{ title }}</h1>

            <!-- message -->
            <message v-if="message" :message="message"/>

            <!-- add new note -->
            <newNote :note="note" @addNote="addNote"/>

            <div class="note-header">
              <!-- search -->
              <search :value="search"
              placeholder="Find your note"
              @search="search = $event"/>

              <!-- icons control -->
              <div class="icons">
                <svg :class="{active: grid }" @click="grid = true" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                <svg :class="{active: !grid }" @click="grid = false" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
              </div>
            </div>

            <!-- note list -->
            <notes :notes="notesFilter" :grid="grid" @remove="removeNote"/>

          </div>
        </section>
      </div>
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'
export default {
  components: {
    message,
    newNote,
    notes,
    search
  },
  data() {
    return{
      title: 'Notes App',
      search: '',
      message: null,
      grid: true,
      note: {
        title: '',
        description: ''
      },
      notes: [{
        title:  'First Note',
        description: 'Description for first Note',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title:  'Second Note',
        description: 'Description for second Note',
        date: new Date(Date.now()).toLocaleString()
      },
      {
        title:  'Third Note',
        description: 'Description for third Note',
        date: new Date(Date.now()).toLocaleString()
      }
    ]
}
},
computed: {
  notesFilter() {
    let array = this.notes
    let search = this.search
    if (!search) return array

    search = search.trim().toLowerCase()

    //Filter
    array = array.filter(function (item) {
      if (item.title.toLowerCase().indexOf(search) !== -1) {
        return item
      }
    })
    //error
    return array
  }
},
methods: {
  addNote() {
    let {title, description} = this.note

    if (title == '' || description == '' ) {
      this.message = 'Title and description can not be empty'
      return false
    }
    this.notes.push({
      title,
      description,
      date: new Date(Date.now()).toLocaleString()
    })
    this.note.title = '' ;
    this.note.description = ''
    this.message = null
  },
  removeNote(index){
    this.notes.splice(index, 1)
  }
}

}
</script>

<style lang="scss" scoped>
h1{
  font-size: 32px;
}
.note-header{
  svg{
    margin-right: 12px;
    color: #999999;
    &.active{
      color: #402caf;
    }
    &:last-child{
      margin-right: 0
    }
  }
}
</style>
