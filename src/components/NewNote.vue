<template lang="html">
  <div class="new-note">
    <label>Title</label>
    <div class="title-priority">
      <div class="title">
        <input type="text" v-model="note.title">
        <input type="hidden" v-model="note.edit" value=false>
        <input type="hidden" v-model="note.editDescription" value=false>
      </div>
      <div class="priority">
        <select required v-model="note.priority">
            <option value="" disabled>Select priority</option>
            <option value="standart">Standart</option>
            <option value="high">High</option>
            <option value="veryHigh">Very high</option>
        </select>
      </div>
    </div>
    <label>Description</label>
    <textarea v-model="note.description"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      selected: '',
    }
  },
  props: {
    note: {
      type: Object,
      required: true
    }
  },
  methods: {
    addNote () {
      this.$emit('addNote', this.note)
      console.log(this.note)
    }
  }
}
</script>

<style lang="scss" scoped>
.new-note{
  text-align: center;
}
.title-priority{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.title{
  flex-basis: 75%;
}
.priority {
  flex-basis: 20%;
  margin-top: 5px;
}
.priority select{
  width: 100%;
}
</style>
