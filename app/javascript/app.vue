<template>
  <div id="app">
    <Header />
    <CheckList />
  </div>
</template>

<script>
import Header from './packs/conponents/Header.vue'
import CheckList from './packs/conponents/CheckList.vue'
export default {
  components: {
    CheckList,
    Header
  }
}
</script>

<style scoped>
</style>