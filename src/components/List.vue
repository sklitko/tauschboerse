<template>
  <div class="container">
    <div class="col-md-6 col-xs-12">
    <div class="test">
      <h1>{{ msg }}</h1>
      <h2>Test</h2>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'list',
  data () {
    return {
      msg: 'LIST Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

body {
  background-color: brown;
}

</style>
