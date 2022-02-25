<template>
  <div id="app">
    <HeaderComp @getQuery="requestCombiner"/>
    <MainComp :movies = "movies"/>
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
      endpoint : "https://api.themoviedb.org/3/search/movie?api_key=a7b98ee26673d183ad161034fac46e74&",
      request : "",
      movies : []
    }
  },
  methods: {
    //requestCombiner: mette insieme la richiesta ricevuta dagli input nella header e richiama le api
    requestCombiner(search) {
      this.request = this.endpoint + "&query=" + search;
      this.apiCall();
    },
    apiCall() {
      axios.get(this.request)
      .then((response) => {
        this.movies = response.data.results;
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
