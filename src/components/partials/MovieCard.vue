<template>
  <div class="movieCard">
    <div class="poster">
        <img :src="'https://image.tmdb.org/t/p/w300' + image" :alt="title" v-if="image != null">
        <img src="../../assets/img/placeholder.png" :alt="title" v-else>
    <div class="info">
        <h1>{{title}}</h1>
        <h3>T.O. {{originalTitle}}</h3>
        <lang-flag :iso="language" :squared="false" class="flag"/>
        <font-awesome-icon  v-for="i in 5" :key="i" :icon="(i < vote)? 'fa-star fa-solid' : 'fa-star fa-regular'" />
    </div>
    </div>

    
    <div class="title">
    <h1>{{title}}</h1>
    </div>

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
        margin-bottom: 3rem;
        color: $white;
        width: 250px;


        .poster {
            margin-bottom: 0.5rem;
            width: 100%;
            height: 370px;
            position: relative;

            &:hover .info{
                transition: 300ms;
                opacity: 1;
            }

            img {
                border-radius: 20px;
                object-fit: cover;
                height: 100%;
                width: 100%;
            }

            .info {
                padding: 1rem 0 2rem 0.5rem;
                width: 100%;
                position: absolute;
                bottom: 0;
                background: linear-gradient(0deg, rgba(33,31,31,1) 0%, rgba(33,31,31,0.4990371148459384) 75%, rgba(0,0,0,0.006039915966386533) 100%);
                opacity: 0;

                h3 {
                    font-weight: 100;
                    }

                .fa-star {
                    color: gold;
                    margin-top: 0.5rem;
                }
                
                .flag {
                    margin-right: 1rem;
                }
            }
        }


        .title {
            max-width: 300px;
        }
    }
</style>