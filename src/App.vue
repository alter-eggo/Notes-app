<template>
  <div class="wrapper">
      <div class="wrapper-content">
        <section>
          <div class="container">
            <h1> {{ title }}</h1>
            <message v-if="message" :message="message"/>
            <div class="new-note">
              <input type="text" v-model="note.title">
              <textarea v-model="note.description"> </textarea>
              <span> </span>
              <button @click="addNote">New note</button>
            </div>

            <div class="notes" v-for="(note, index) in notes" :key="index">
              <div class="note-header">
                <p> {{ note.title }} </p>
              </div>
              <div class="note-body">
                <p> {{ note.description }} </p>
                <span> {{ note.date }}</span>
              </div>
            </div>
          </div>
        </section>
      </div>
  </div>
</template>

<script>
import message from '@/components/message.vue'
export default {
  components: {
    message
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
      this.message = 'Title can not be empty'
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
  }

}

}
</script>

<style lang="scss" scoped>
  .wrapper{
    text-align: center;
  }
</style>
