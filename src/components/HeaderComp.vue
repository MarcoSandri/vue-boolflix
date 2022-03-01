<template>
  <header>
      <div class="logo">
            <h1>NETFLIX</h1>
      </div>
      <div class="search">
          <!-- Al rilascio del tasto invio o al click del bottone manda la query scritta nell'input all'app -->
          <input type="text" v-model="search" @keyup.enter="sendQuery" placeholder="search">
          <button @click="sendQuery"> <font-awesome-icon icon="fa-solid fa-magnifying-glass" /> </button>
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
        padding: 1rem;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .logo {
          color: $red;
        }

        .search {
            position: relative;

            input {
                background-color: $primary;
                border: 2px solid gray;
                border-radius: 5px;
                padding: 0.5rem 1rem 0.5rem 2.5rem;
                color: $white;
            }

            button {
                background: none;
                border: none;
                color: $white;
                position: absolute;
                left: 0.75rem;
                top: 50%;
                transform: translate(0, -50%);
                font-size: 1.25rem;
                cursor: pointer;
            }
        }
    }
</style>