<template>
  <div>
    <Header />
    <SearchField />
  </div>
</template>

<script>
import Header from '~/layouts/partials/Header.vue'
import SearchField from '~/layouts/partials/SearchField.vue'

export default {
  components: {
    Header,
    SearchField
  }
}
</script>

<style lang="stylus" scoped>
.container {
  padding: 0;
}
</style>
