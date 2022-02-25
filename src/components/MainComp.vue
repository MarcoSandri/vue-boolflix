<template>
  <main>
      <div class="container">
          <MovieCard v-for="(movie,index) in movies" :key="index" :title="movie.title" :originalTitle="movie.original_title" :language="movie.original_language" :vote="movie.vote_average"/>
      </div>
  </main>
</template>

<script>
import MovieCard from './partials/MovieCard.vue'

export default {
    name: "MainComp",
    components: {
        MovieCard
    },
    props: {
        movies: Array
    }
}
</script>

<style lang="scss">
    @import '../assets/style/colors.scss';

    main {
        display: flex;
        justify-content: center;

        .container {
            width: 70%;
            display: flex;
            flex-wrap: wrap;
            justify-content: flex-start;



        }
    }

</style>
