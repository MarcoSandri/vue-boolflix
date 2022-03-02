<template>
  <div id="app">
    <HeaderComp @getQuery="requestCombiner" class="header" />
    <MainComp :movies = "movies" :series = "series" class="main" :movieGenres="movieGenres" :serieGenres="serieGenres"/>
  </div>
</template>

<script>
const axios = require('axios');

import MainComp from './components/MainComp.vue'
import HeaderComp from './components/HeaderComp.vue'

export default {
  name: 'App',
  components: {
    MainComp,
    HeaderComp
  },

  data() {
    return {
      key: "a7b98ee26673d183ad161034fac46e74",
      movies : [],
      series : [],
      movieGenres: [],
      serieGenres: []
    }
  },

  computed: {

  },
  methods: {

    //requestCombiner: mette insieme la richiesta ricevuta dagli input nella header e richiama le api
    requestCombiner(search) {
      const parametri = {
        params: {
        'api_key' : this.key,
        'query' : search,
        'language' : "it-IT"
        }
      };
      this.movies = [];
      this.series = [];
      this.movieCall(parametri);
      this.seriesCall(parametri);
      this.genreIdCall();
    },

    //Ricerca i film
    movieCall(params) {
      axios.get('https://api.themoviedb.org/3/search/movie/', params)
      .then((response) => {
        this.movies = response.data.results;
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });
    },

    //Ricerca le serie tv
    seriesCall(params) {
      axios.get('https://api.themoviedb.org/3/search/tv/', params)
      .then((response) => {
        this.series = response.data.results;
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });
    },
    
    genreIdCall() {
      axios.get('https://api.themoviedb.org/3/genre/tv/list?api_key=a7b98ee26673d183ad161034fac46e74&language=it-IT')
      .then((response) => {
        this.serieGenres = response.data.genres;
        console.log(this.serieGenres);
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });

      axios.get('https://api.themoviedb.org/3/genre/movie/list?api_key=a7b98ee26673d183ad161034fac46e74&language=it-IT')
      .then((response) => {
        this.movieGenres = response.data.genres;
        console.log(this.serieGenres);
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });
    }
  }

}
</script>

<style lang="scss">
@import './assets/style/general.scss';

</style>
