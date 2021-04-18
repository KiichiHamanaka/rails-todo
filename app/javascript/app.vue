<template>
  <div id="app">
    {{json}}
  </div>
</template>

<script>
import axios from "axios";

export default {
  data () {
    return {
      json: null
    }
  },
  mounted () {
    axios
        .get('http://localhost:5000/api/tasks')
        .then(response => (this.json = response))
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>