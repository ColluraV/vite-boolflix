<script >
import StarRating from 'vue-star-rating'
import { store, discoverMovies, takeFlags } from '../store'
export default {

    data() {
        return {
            store,

        };
    },


    components: {
        StarRating,
    },

    methods: {
        takeFlags,
        takeImg(imgs) {
            if (imgs == null) {
                return `https://d994l96tlvogv.cloudfront.net/uploads/film/poster/poster-image-coming-soon-placeholder-no-logo-500-x-740_29376.png`
            }
            return `https://image.tmdb.org/t/p/original/` + imgs
        },
        voteConvert(voto) {
            return (voto / 2)
        },

        discoverMovies,

    },
    mounted() {
        discoverMovies()
    },

};


</script>

<template>
    <div id="moviesScroll" class="container-fluid">
        <div class="" v-for="carta in store.movies">

            <div class="card h-100 mx-3" style="width: 18rem;">
                <img class="card-img-top h-100 relative" v-bind:src="takeImg(carta.poster_path)">
                <div class="flex-column overflowy card-body hidden">
                    <h5 class="card-title">{{ carta.title }}</h5>
                    <p class="card-text">Original Title: {{ carta.original_title }}</p>

                    <p class="card-text">Lingua Originale: {{ carta.original_language }}

                        <img alt="" v-bind:src="takeFlags(carta.original_language)">

                    </p>
                    <star-rating :increment="0.01" :fixed-points="2" :rating="voteConvert(carta.vote_average)"
                        :read-only="true" :star-size="45"></star-rating>

                    <p class="card-text my-3 overflowy">Lore: {{ carta.overview }}</p>

                </div>
            </div>

        </div>

    </div>
</template>

<style lang="scss" scoped>
@use "../src/styles/partials/variables" as *;
</style>
