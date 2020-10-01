<template>
  <div>
    <v-row no-gutters> <nuxt-link to="/"> Home</nuxt-link>/{{ Name }} </v-row>
    <v-row nogutters>
      <v-col cols="2">
        <v-img :src="img"></v-img>
      </v-col>
      <v-col cols="8">
        <v-list-item>Language : {{ Language }}</v-list-item>
        <v-list-item>Release Date : {{ Release }}</v-list-item>
        <v-list-item>Average vote : {{ average }}</v-list-item>
        <v-list-item>Overview : {{ Overview }}</v-list-item>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <v-card>
          <v-list-item-group>
            <v-list-item v-for="movie in movieList" :key="movie.id">
              <v-img :src="movie.poster_path" max-width="50"></v-img>
              <p>{{ movie.title }}</p>
            </v-list-item>
          </v-list-item-group>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<style></style>

<script>
import axios from 'axios'
export default {
  components: {},
  data() {
    return {
      tmp: null,
      Name: this.$route.params.id.title,
      Release: this.$route.params.id.release_date,
      Language: this.$route.params.id.original_language,
      Overview: this.$route.params.id.overview,
      img: this.$route.params.id.poster_path,
      average: this.$route.params.id.vote_average,
    }
  },
  methods: {
    seeMore() {
      axios
        .get(
          'https://api.themoviedb.org/3/search/movie?api_key=ea1e4e94cd0464ac689ddcc8affadfb6&query=+' +
            this.textSearch
        )
        .then((res) => {
          this.movieList = res.data.results
          console.log(this.movieList)
        })
        .catch((err) => {
          console.error(err)
        })
    },
  },
}
</script>
