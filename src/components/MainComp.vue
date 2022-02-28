<template>
  <main>
      <div class="container">
                <h1 v-if="movies.length > 0">MOVIES</h1>
            <section class="movies">
                <MovieCard
                v-for="(movie,index) in movies" 
                :key="index"
                :image="'https://image.tmdb.org/t/p/w342' + movie.poster_path"
                :title="movie.title" 
                :originalTitle="movie.original_title" 
                :language="movie.original_language" 
                :vote="Math.round(movie.vote_average)/2"/>
            </section>
                <h1 v-if="series.length > 0">SERIES</h1>
            <section class="series">
                <MovieCard 
                v-for="(serie,index) in series" 
                :key="index"
                :image="'https://image.tmdb.org/t/p/w342' + serie.poster_path"
                :title="serie.name" 
                :originalTitle="serie.original_name" 
                :language="serie.original_language" 
                :vote="Math.round(serie.vote_average)/2"/>
            </section>
      </div>
  </main>
</template>

<script>
import MovieCard from './partials/MovieCard.vue';

export default {
    name: "MainComp",
    components: {
        MovieCard
    },
    props: {
        movies: Array,
        series: Array
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

            section {
                display: flex;
                flex-wrap: wrap;
                justify-content: flex-start;
            }



        }
    }

</style>
