<template lang="html">
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      requred: false,
  }
}
}
</script>

<style lang="scss" scoped>
.message {
  text-align: center;
  padding: 20px;
}
</style>
