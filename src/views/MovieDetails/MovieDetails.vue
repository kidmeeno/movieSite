<script>
import Header from '../../components/Header.vue'
import MovieCarousel from '../../components/MovieCarousel.vue'
import MovieDetailSection from '../../components/MovieDetailSection.vue'
import UsersCarouselVue from '../../components/UsersCarousel.vue'
import LoaderVue from '../../components/Loader.vue'
import TabNavVue from '../../components/TabNav.vue'
import AppLayoutVue from '../../components/AppLayout.vue'




export default {
    components: { Header, AppLayoutVue, MovieCarousel, MovieDetailSection, UsersCarouselVue, LoaderVue, TabNavVue },
    data() {
        return {
            movieDetails: {},
            movieActors: [],
            inTheaters: [],
            isLoading: true,
            categories: {
                movieCast: 'Cast',
                movieLikes: 'You might also like',
            },
        }
    },
    computed: {
        fetchData() {
            const catchedMovieActors = JSON.parse(localStorage.getItem("movieActors"));
            const movieId = this.$route.query.id;
            fetch(`https://imdb-api.com/API/FullCast/k_b8d5c0ak/${movieId}`)
                .then(response => response.json())
                .then(response => {
                    const actors = response.actors;
                    const dataToSave = { ...catchedMovieActors, [movieId]: actors }
                    // basically catching the data here for future use
                    localStorage.setItem("movieActors", JSON.stringify(dataToSave));
                    this.movieDetails = this.$route.query
                    this.movieActors = response.actors
                    this.isLoading = false;
                })
                .catch(err => {
                    this.isLoading = false;
                    console.error(err)
                });

        }
    },
    mounted() {
        /* due to the fact that IMDB have restriction to a number of request you can make to there api in a space of 24hours, 
        I decided to catch the first data gotten for development purpose. This will not be the case for  life project.*/
        const catchedMovieActors = JSON.parse(localStorage.getItem("movieActors"));
        const catchedMovieData = JSON.parse(localStorage.getItem("movieData"));
        const movieId = this.$route.query.id;
            this.inTheaters = catchedMovieData[2].items;
        if (!movieId) {
            router.push('/');
            return
        }
        if (!catchedMovieActors) {
            localStorage.setItem("movieActors", JSON.stringify({}));
            this.fetchData
            console.log(movieId,"movieId",catchedMovieActors);
        }
        if (catchedMovieActors[movieId]) {
            this.movieActors = catchedMovieActors[movieId]
            this.movieDetails = this.$route.query
            this.isLoading = false;
            return
        }
        this.fetchData
    },
}
</script>

<template>
    <AppLayoutVue>
        <div class="d-none d-md-block" v-if="!isLoading">
            <MovieDetailSection :hideLearnBtn="true" :movieDetails="movieDetails" />
            <UsersCarouselVue :casts="movieActors" :title="categories.movieCast" />
            <MovieCarousel :moviesTitle='categories.movieLikes' :movies="inTheaters" />
        </div>
        <div class="d-md-none d-block" v-if="!isLoading">
            <MovieDetailSection :hideLearnBtn="true" :movieDetails="movieDetails" />
            <TabNavVue :casts="movieActors" :movies="inTheaters" />
        </div>
        <div v-else>
            <LoaderVue/>
        </div>
    </AppLayoutVue>
</template>
