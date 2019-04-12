<template lang="html">
  <div class="notes">
    <div class="note" :class="{full: !grid, 'high-priority': note.priority == 'high', 'very-high-priority': note.priority == 'veryHigh' }" v-for="(note, index) in notes" :key="index">
      <div class="note-header" :class="{full: !grid}">
        <p style="cursor: pointer;" v-if="!note.edit" @click="editTitle(index)"> {{ note.title }} </p>
        <input type="text" v-if="note.edit" v-model="notes[index].titleEdited" value="notes[index].title">
        <p style="cursor: pointer;" @click="removeNote(index)">X</p>
      </div>
      <div class="note-body">
        <p style="cursor: pointer;" v-if="!note.editDescription" @click="editDescr(index)"> {{ note.description }} </p>
        <input type="text" v-if="note.editDescription" v-model="notes[index].descrEdited" value="notes[index].description">
        <span> {{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    },
    titleEdited: {
      type: String,
      required: false
    },
    descrEdited: {
      type: String,
      required: false
    }
  },
  methods: {
    removeNote(index){
      console.log(`Note id - ${index} removed`);
      this.$emit('remove', index)
    },
    editTitle(index){
      this.$emit('editTitle', index, this.notes[index].titleEdited)
    },
    editDescr(index){
      this.$emit('editDescr', index, this.notes[index].descrEdited)
    },
  },
  computed: {
  }
}
</script>

<style lang="scss">
.notes{
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #ffffff;
  &.full{
    width: 100%;
    text-align: center;
  }
  &:hover{
    box-shadow: 0 30px 30px rgba(0, 0, 0, .04);
    transform: translate(0, -6px);
    transition: 0.2s;
  }
}
.note-body{
  p {
    margin: 20px 0;
  }
  span {
    font-size: 15px;
    color: #999999;
  }
}
.note-header{
  display: flex;
  align-items: center;
  justify-content: space-between;
  &.full{
    justify-content: center;
  }
  p{
    font-size: 20px;
    color: #402caf;
    margin-right: 16px;
  }
}
.high-priority{
  &:hover{
  box-shadow: 0 30px 30px rgba(255, 196, 0, 0.5);
}
}

.very-high-priority{
  &:hover{
  box-shadow: 0 30px 30px rgba(255, 3, 3, 0.5);
}
}
</style>
