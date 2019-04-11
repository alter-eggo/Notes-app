<template lang="html">
  <div class="notes">
    <div class="note" :class="{full: !grid}" v-for="(note, index) in notes" :key="index">
      <div class="note-header" :class="{full: !grid}">
        <p> {{ note.title }} </p>
        <p style="cursor: pointer;" @click="removeNote(index)">X</p>
      </div>
      <div class="note-body">
        <p> {{ note.description }} </p>
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
    }
  },
  methods: {
    removeNote(index){
      console.log(`Note id - ${index} removed`);
      this.$emit('remove', index)
    }
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
</style>
