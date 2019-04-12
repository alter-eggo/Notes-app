<template>
  <div class="wrapper">
      <div class="wrapper-content">
        <section>
            <div class="container">
              <div class="escArea">
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
              </div>
            <!-- note list -->
            <notes :notes="notesFilter" :grid="grid" @remove="removeNote" :edit="edit" @editTitle="editTitle" :titleEdited="titleEdited" :editDescription="editDescription" @editDescr="editDescr" :descrEdited="descrEdited"/>
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
      edit: false,
      editDescription: false,
      titleEdited: '',
      descrEdited: '',
      note: {
        title: '',
        description: '',
        priority: '',
      },
      notes: [{
        title:  'First Note',
        description: 'Description for first Note',
        date: new Date(Date.now()).toLocaleString(),
        edit: false,
        editDescription: false
      },
      {
        title:  'Second Note',
        description: 'Description for second Note',
        date: new Date(Date.now()).toLocaleString(),
        edit: false,
        editDescription: false

      },
      {
        title:  'Third Note',
        description: 'Description for third Note',
        date: new Date(Date.now()).toLocaleString(),
        edit: false,
        editDescription: false
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
    let {title, description, priority} = this.note

    if (title == '' || description == '' ) {
      this.message = 'Title and description can not be empty'
      return false
    }

    if (priority == '') {
      this.message = 'Please select priority'
      return false
    }

    this.notes.push({
      title,
      description,
      priority,
      edit:false,
      date: new Date(Date.now()).toLocaleString()
    })
    this.note.title = ''
    this.note.description = ''
    this.message = null
    this.note.priority = ''
  },
  removeNote(index){
    this.notes.splice(index, 1)
  },
  editTitle(index){
    this.notes[index].edit = true;
    document.body.addEventListener('keyup', e => {
      if (e.keyCode === 13) {
        this.notes[index].title = this.notes[index].titleEdited;
        this.notes[index].date = new Date(Date.now()).toLocaleString();
        this.notes[index].edit = false;
    }
  })
    document.body.addEventListener('keyup', e => {
      if (e.keyCode === 27) {
        this.notes[index].edit = false;
    }
  })
    // document.querySelector('.escArea').addEventListener('click', () => {
    //     this.notes[index].edit = false;
    // })
},
  editDescr(index){
    this.notes[index].editDescription = true;
    document.body.addEventListener('keyup', e => {
      if (e.keyCode === 13) {
        this.notes[index].description = this.notes[index].descrEdited;
        this.notes[index].date = new Date(Date.now()).toLocaleString();
        this.notes[index].editDescription = false;
    }
  })
    document.body.addEventListener('keyup', e => {
      if (e.keyCode === 27) {
        this.notes[index].editDescription = false;
    }
  })
    // document.querySelector('.escArea').addEventListener('click', () => {
    //     this.notes[index].editDescription = false;
    // })
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
