<template>
  <v-footer dark height="auto">
    <v-card class="flex" flat tile>
      <v-card-actions class="grey darken-3">
        {{ information }}
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
