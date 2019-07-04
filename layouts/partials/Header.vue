<template>
  <v-layout class="header" row wrap justify-center>
    <v-flex xs12>
      <v-card>
        <v-img
          class="white--text"
          height="200px"
          src="https://wallpaperaccess.com/full/193203.jpg"
        >
          <v-container fill-height fluid>
            <v-layout fill-height>
              <v-flex xs12 align-end flexbox> </v-flex>
            </v-layout>
          </v-container>
        </v-img>
        <v-card-actions>
          <a
            href="https://github.com/Acquati/recrutamento-fullstack"
            target="_blank"
          >
            <v-btn color="blue-grey" class="white--text">
              github
              <v-icon right dark>code</v-icon>
            </v-btn>
          </a>
        </v-card-actions>
        <v-card-actions>
          <a href="https://developer.marvel.com/" target="_blank">
            <v-btn color="red" class="white--text"
              >marvel developer
              <v-icon right dark>gavel</v-icon>
            </v-btn>
          </a>
        </v-card-actions>
        <v-card-title>
          <div>
            {{ description }}
          </div>
        </v-card-title>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      description:
        'Pesquise sobre as mais diversas personagens do Universo Marvel: mulheres, homens, organizações, espécies alienigenas, divindades, animais, entidades não-corporais, manifestações trans-dimensionais, personificações abstratas e bolhas amorfas verdes que ocupam o Universo Marvel (e vários universos alternativos, linhas do tempo e realidades alteradas). Por exemplo, o Homem-Aranha.'
    }
  }
}
</script>

<style lang="stylus" scoped>
.header {
  margin-bottom: 3rem;

  a {
    text-decoration: none;
  }
}
</style>
