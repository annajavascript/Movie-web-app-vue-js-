<template>
    <div class="container">
        <div class="row mt-4">
            <div class="col-md-12">
                <div v-for="(movie, key) in getFavoriteMovieList" :key="key" class="mt-4 d-flex align-items-center flex-column">
                    <div class="bg-white mb-3 shadow-sm rounded d-flex" style="width: 700px; height: 250px;">
                        <img style="height:100%; width:168px; border-radius: .25rem 0px 0px .25rem" :src="movie.Poster !== 'N/A' ? movie.Poster : 'https://i.hizliresim.com/a3258ou.png'">
                        <div style="padding: 20px;">
                            <h2>{{ movie.Title }}</h2>
                            <div>
                                <small><strong>Type:</strong>  {{ movie.Type | capitalize }}</small>
                            </div>
                            <div>
                                <small><strong>Year:</strong> {{ movie.Year }}</small>
                            </div>
                            <router-link :to="{ name: 'movie', params: { id: movie.imdbID } }" tag="button" class="btn text-light btn-sm mt-3" style="background: #000">Show Details</router-link>
                            <a :href="`https://www.imdb.com/title/${movie.imdbID}`" target="_blank"><button class="btn text-light btn-sm mt-3" style="background: #000;  margin-left: 5px">IMDB</button></a>
                            <button v-if="getFavoriteMovie(movie.imdbID)" @click="removeFavoriteMovie(movie)" class="btn text-light btn-sm mt-3" style="background: #ce181e;  margin-left: 5px">Remove from Favorites</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
    data() {
        return {
            pageTitle: 'My Favorites - Movie',
        };
    },
    computed: {
        ...mapGetters(['getFavoriteMovieList', 'getFavoriteMovie']),
    },
    methods: {
        ...mapActions(['removeFavoriteMovie']),
    },
    created() {
        document.title = this.pageTitle;
    },
};
</script>
