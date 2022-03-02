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
      series : [],
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
      this.movieCall(parametri);
      this.seriesCall(parametri);
    },

    //Ricerca i film
    movieCall(params) {
      axios.get('https://api.themoviedb.org/3/search/movie/', params)
      .then((response) => {
        let moviesTemp = [];
        moviesTemp = response.data.results;
        this.addActors('movie', moviesTemp);
        this.movies = moviesTemp;
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
        let seriesTemp = [];
        seriesTemp = response.data.results
        this.addActors('tv', seriesTemp);
        this.series = seriesTemp;
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });
    },

    //Ricerca gli attori
    actorCall(id, type) {
      let ActorsArray  = [];
      axios.get(`https://api.themoviedb.org/3/${type}/${id}/credits?api_key=a7b98ee26673d183ad161034fac46e74`)
      .then((response) => {
        for(let i = 0; i < 5; i++) {
          ActorsArray.push(response.data.cast[i].name);
        }
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });
      return ActorsArray;
    },

    addActors(type, array) {
      for(let i = 0; i < array.length; i++) {
        array[i].actors = this.actorCall(array[i].id, type)
      }
    }
  }

}
</script>

<style lang="scss">
@import './assets/style/general.scss';

</style>
