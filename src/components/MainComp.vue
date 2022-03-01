<template>
  <main>
      <div class="container">
                <h1 class="sectiontitle" v-if="movies.length > 0">FILM</h1>
            <section class="movies">
                <MovieCard
                v-for="(movie,index) in movies" 
                :key="index"
                :image="movie.poster_path"
                :title="movie.title" 
                :originalTitle="movie.original_title" 
                :language="movie.original_language" 
                :vote="Math.round(movie.vote_average)/2"/>
            </section>
                <h1 class="sectiontitle" v-if="series.length > 0">SERIE</h1>
            <section class="series">
                <MovieCard 
                v-for="(serie,index) in series" 
                :key="index"
                :image="serie.poster_path"
                :title="serie.name" 
                :originalTitle="serie.original_name" 
                :language="serie.original_language" 
                :vote="Math.round(serie.vote_average/2)"/>
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
        background: linear-gradient(0deg, rgba(33,31,31,1) 0%, rgba(33,31,31,1) 80%, rgba(0,0,0,1) 100%);
        height: calc(100vh - 70px);
        overflow: auto;

        &::-webkit-scrollbar {
            width: 12px;
        }
        &::-webkit-scrollbar-track {
            background: $primary;
        }
        &::-webkit-scrollbar-thumb {
            background-color: #505050;    /* color of the scroll thumb */
            border-radius: 20px;       /* roundness of the scroll thumb */
            border: 3px solid $primary;  /* creates padding around scroll thumb */
        }


        .container {
            width: 70%;

            .sectiontitle {
                color: $red;
                margin: 1rem 0;
                font-size: 4em;
            }

            section {
                display: flex;
                flex-wrap: wrap;
                justify-content: space-between;
            }



        }
    }

</style>
