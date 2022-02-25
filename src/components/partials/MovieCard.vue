<template>
  <div class="movieCard">
      <h1>{{title}}</h1>
      <h2>{{originalTitle}}</h2>
      <span>{{language}}</span>
      <span>{{vote}}</span>
  </div>
</template>

<script>
export default {
    name: "MovieCard",
    props: {
        title: String,
        originalTitle: String,
        language: String,
        vote: String
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