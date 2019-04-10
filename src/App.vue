<template>
  <div class="wrapper">
      <div class="wrapper-content">
        <section>
          <div class="container">
            <h1> {{ title }}</h1>
            <message v-if="message" :message="message"/>
            <newNote
            :note="note"
            @addNote="addNote"
            />
            <notes :notes="notes" @remove="removeNote"/>
          </div>
        </section>
      </div>
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'

export default {
  components: {
    message,
    newNote,
    notes
  },
  data() {
    return{
      title: 'Notes App',
      message: null,
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

</style>
