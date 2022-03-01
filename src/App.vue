<template>
  <div id="app">
    <HeaderComp @getQuery="requestCombiner" class="header" />
    <MainComp :movies = "movies" :series = "series" class="main" />
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
      series : []
    }
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
      this.movieCall(parametri);
      this.seriesCall(parametri);
    },
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
    seriesCall(params) {
      axios.get('https://api.themoviedb.org/3/search/tv/', params)
      .then((response) => {
        this.series = response.data.results;
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
