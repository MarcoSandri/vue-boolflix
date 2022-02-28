<template>
  <div id="app">
    <HeaderComp @getQuery="requestCombiner"/>
    <MainComp :movies = "movies" :series = "series"/>
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
      endpoint : "https://api.themoviedb.org/3/search/",
      key: "?api_key=a7b98ee26673d183ad161034fac46e74&",
      Mrequest : "",
      Srequest : "",
      movies : [],
      series : [],
    }
  },
  methods: {
    //requestCombiner: mette insieme la richiesta ricevuta dagli input nella header e richiama le api
    requestCombiner(search) {
      this.Mrequest = this.endpoint + "movie" + this.key + "&query=" + search;
      this.Srequest = this.endpoint + "tv" + this.key + "&query=" + search;
      this.movieCall();
      this.seriesCall();
    },
    movieCall() {
      axios.get(this.Mrequest)
      .then((response) => {
        this.movies = response.data.results;
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });
    },
    seriesCall() {
      axios.get(this.Srequest)
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
