<template>
  <v-layout class="header" row wrap justify-center>
    <v-flex xs12>
      <p>{{ hi }}</p>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      hi: 'Hi'
    }
  }
}
</script>

<style lang="stylus" scoped>
.header {}
</style>
