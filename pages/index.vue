<template>
  <div>
    <Header />
    <SearchField />
    <Footer />
  </div>
</template>

<script>
import Header from '~/layouts/partials/Header.vue'
import SearchField from '~/layouts/partials/SearchField.vue'
import Footer from '~/layouts/partials/Footer.vue'

export default {
  components: {
    Header,
    SearchField,
    Footer
  }
}
</script>

<style lang="stylus" scoped>
.container {
  padding: 0;
}
</style>
