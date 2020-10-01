<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <Movie />
    </v-col>
  </v-row>
</template>

<script>
import Movie from '@/pages/Movie.vue'

export default {
  components: {
    Movie,
  },
}
</script>
