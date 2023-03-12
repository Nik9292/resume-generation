<template>
  <h1>Резюме {{ text }}</h1>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
