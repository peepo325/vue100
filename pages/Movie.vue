<template>
  <div>
    <v-row>
      <v-col cols="10">
        <v-text-field label="" solo v-model="textSearch"></v-text-field>
      </v-col>
      <v-col cols="2">
        <v-btn @click="search()" large><v-icon>mdi-magnify</v-icon></v-btn>
      </v-col>
    </v-row>

    <v-row>
      <v-col v-for="movie in movieList" :key="movie.id" :title="movie.title">
        <nuxt-link :to="{ name: 'id-id', params: { id: movie } }">
          <v-hover v-slot:default="{ hover }">
            <v-card flat tile class="d-flex" :elevation="hover ? 12 : 2">
              <v-img
                :src="movie.poster_path"
                aspect-ratio="1"
                class="grey lighten-2 rounded"
              >
                <p class="font-weight-bold grey" style="color: white">
                  {{ movie.title }}
                </p>
              </v-img>
            </v-card>
          </v-hover>
        </nuxt-link>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      movieList: null,
      textSearch: '',
    }
  },
  methods: {
    search() {
      axios
        .get(
          'https://api.themoviedb.org/3/search/movie?api_key=ea1e4e94cd0464ac689ddcc8affadfb6&query=+' +
            this.textSearch
        )
        .then((res) => {
          this.movieList = res.data.results
          this.$$emit('movieList', Object(res.data.results))
        })
        .catch((err) => {
          console.log(err)
        })
    },
  },
}
</script>

<style></style>
