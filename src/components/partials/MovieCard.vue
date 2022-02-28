<template>
  <div class="movieCard">
      <img :src="image" :alt="title">
      <h1>{{title}}</h1>
      <h3>{{originalTitle}}</h3>
      <lang-flag :iso="language"/>
      <span>{{vote}}</span>
      <font-awesome-icon icon="fa-solid fa-star" v-for="(number,index) in Math.floor(vote)" :key="index"/>
      <font-awesome-icon icon="fa-solid fa-star-half" v-for="(number,index) in vote%1" :key="index"/>
  </div>
</template>

<script>

//componente per gestire le bandiere automaticamente
import LangFlag from 'vue-lang-code-flags';

export default {
    name: "MovieCard",
    props: {
        title: String,
        originalTitle: String,
        language: String,
        vote: Number,
        image: String
    },
    components: {
        LangFlag
    }
}
</script>

<style lang="scss">
    @import '../../assets/style/colors.scss';

    .movieCard {
        padding: 1rem;
        max-width: 200px;
        color: $white;
        background-color: $secondary;
    }
</style>