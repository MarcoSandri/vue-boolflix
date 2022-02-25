<template>
  <header>
      <div class="logo">
            <h1>NETFLIX</h1>
      </div>
      <div class="search">
          <!-- Al rilascio del tasto invio o al click del bottone manda la query scritta nell'input all'app -->
          <input type="text" v-model="search" @keyup.enter="sendQuery">
          <button @click="sendQuery">SEARCH</button>
      </div>
  </header>
</template>

<script>
export default {
    name: "HeaderComp",
    data() {
        return {
            search: ""
        }
    },
    methods: {
        //sendQuery: Manda l'input di search all'app
        sendQuery() {
            this.$emit('getQuery', this.search)
        }
    }
}
</script>

<style lang="scss">
    @import '../assets/style/colors.scss';

    header {
        background-color: $secondary;
        color: $red;
        padding: 1rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>