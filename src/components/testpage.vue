<template>
  <div class="hi">
    {{ msg }}
  </div>

</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Test Page'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
