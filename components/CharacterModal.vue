<template>
  <div>
    <v-btn color="red" dark @click.stop="dialog = true">
      know more
      <v-icon right dark>library_books</v-icon>
    </v-btn>

    <v-dialog
      v-model="dialog"
      width="800px"
      :fullscreen="$vuetify.breakpoint.smAndDown"
    >
      <v-card>
        <v-card-title class="headline" primary-title>
          {{ character.name }}
        </v-card-title>

        <v-card-text v-if="character.description">
          {{ character.description }}
        </v-card-text>
        <v-card-text v-else>
          No description for this character was found on Marvel API.
        </v-card-text>

        <div v-for="(item, index) in character.urls" :key="index">
          <v-card-title class="title text-capitalize pb-0">
            {{ item.type }}
          </v-card-title>
          <v-card-text class="subheading text-truncate">
            <a :href="item.url" target="_blank">{{ item.url }}</a>
          </v-card-text>
        </div>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn flat @click="dialog = false">
            <v-icon right>clear</v-icon>
          </v-btn>
        </v-card-actions>

        <v-img
          :src="character.thumbnail.path + '.' + character.thumbnail.extension"
        ></v-img>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    character: {
      default: () => [],
      type: Object
    }
  },
  data() {
    return {
      dialog: false
    }
  }
}
</script>

<style lang="stylus" scoped></style>
