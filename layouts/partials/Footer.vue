<template>
  <v-footer dark height="auto">
    <v-card class="flex" flat tile>
      <v-card-title class="teal">
        <strong class="subheading">{{ information }}</strong>
      </v-card-title>

      <v-card-actions class="grey darken-3 justify-center">
        &copy;2019<strong>Marvel</strong>
      </v-card-actions>
    </v-card>
  </v-footer>
</template>

<script>
export default {
  data() {
    return {
      information:
        'Developed by Leandro Acquati, with nice tools like Vue, Vuetify, Nuxt, Google Cloud and Marvel Developer.'
    }
  }
}
</script>

<style lang="stylus" scoped></style>
