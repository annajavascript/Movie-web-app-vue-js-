<template>
    <div class="container">
        <div class="row">
             <div class="col-md-12 d-flex justify-content-center">
                <form>
                    <div class="bg-white mt-5 rounded shadow-sm d-flex justify-content-between bar p-3 align-items-center" style="width: 700px; height: 60px;">
                        <input type="text" v-model="movieId" class="form-control" style="width: 100%" placeholder="Enter Movie Id">
                          <router-link :to="{ name: 'movie', params: { id: movieId } }" tag="button" class="btn text-light btn-sm" style="margin-left: 15px;background: #000">Search</router-link>
                    </div>
                </form>
            </div>
             <div class="col-md-12 mt-3 d-flex justify-content-center">
                <form>
                    <div class="bg-white mt-5 rounded shadow-sm d-flex justify-content-between bar p-3 align-items-center" style="width: 700px; height: 60px;">
                        <input type="text" v-model="movie"  @keyup='search' class="form-control" style="width: 100%" placeholder="Enter Movie Title or series">
                        <!-- <button @click.prevent="search"  class="btn text-light" style="margin-left: 15px;background: #000">Search</button> -->
                    </div>
                </form>
            </div>
        </div>
        <router-view></router-view>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
    data() {
        return {
            pageTitle: 'Search - Movie',
            movie: this.$route.params.searchedMovie ? this.$route.params.searchedMovie : '',
            movieId: '',
            movieInfo: [],
            apiKey: 'ae1703d5',
        };
    },
    methods: {
        search() {
            this.$router.push({ name: 'search', params: { searchedMovie: this.movie } });
        },

        searchById() {
            this.$store.dispatch('fetchMovie', this.movieId);
        },
    },
    computed: {

    },
    created() {
        document.title = this.pageTitle;
    },
};
</script>

<style scoped>
    @media(max-width: 600px) {
        .bar {
            width: 100% !important;
        }
    }
</style>
