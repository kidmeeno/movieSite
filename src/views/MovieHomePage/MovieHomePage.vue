<script>
import Header from '../../components/Header.vue'
import MovieCarousel from '../../components/MovieCarousel.vue'
import MovieDetailSection from '../../components/MovieDetailSection.vue'
import LoaderVue from '../../components/Loader.vue'
import AppLayoutVue from '../../components/AppLayout.vue'



export default {
    components: { Header, AppLayoutVue, MovieCarousel, MovieDetailSection, LoaderVue },
    data() {
        return {
            popularMovies: [],
            popularTvMovies: [],
            inTheaters: [],
            isLoading: true,
            moviesCategories: {
                MostPopularMovies: 'Most Popular Movies',
                MostPopularTVs: 'Most Popular TVs',
                inTheaters: 'In Theaters',
            },
            movieToDisplay: {},
        };
    },
    computed: {
        fetchData() {
            const urls = [
                'https://imdb-api.com/API/MostPopularMovies/k_b8d5c0ak',
                'https://imdb-api.com/API/MostPopularTVs/k_b8d5c0ak',
                'https://imdb-api.com/API/InTheaters/k_b8d5c0ak'
            ]

            const requests = urls.map(url => fetch(url))

            Promise.all(requests)
                .then(responses => Promise.all(responses.map(res => res.json())))
                .then(response => {
                    // setting the state based on the currect field is determined by the way we have our url in the array of urls.
                    localStorage.setItem("movieData", JSON.stringify(response));
                    this.popularMovies = response[0].items;
                    this.popularTvMovies = response[1].items;
                    this.inTheaters = response[2].items;
                    this.movieToDisplay = this.displayOneMovie(response[2].items);
                    this.isLoading = false;
                })
                .catch(error => {
                    this.isLoading = false;
                    console.error(err)
                })
        }
    },
    methods: {
        displayOneMovie: (movie) => {
            return movie[movie.length - 1]
        }
    },
    mounted() {
        /* due to the fact that IMDB have restriction to a number of request you can make to there api, 
        I decided to catch the first data gotten for development purpose. This will not be the case for  life project.*/
        const catchedMovieData = localStorage.getItem("movieData");
        if (!catchedMovieData) {
            this.fetchData
        } else {
            const data = JSON.parse(catchedMovieData);
            this.popularMovies = data[0].items;
            this.popularTvMovies = data[1].items;
            this.inTheaters = data[2].items;
            this.movieToDisplay = this.displayOneMovie(data[2].items);
            this.isLoading = false;
        }
    },
};
</script>

<template>
    <AppLayoutVue>
        <div v-if="!isLoading">
            <MovieDetailSection :movieDetails="movieToDisplay" />
            <MovieCarousel :moviesTitle='moviesCategories.inTheaters' :movies="inTheaters" />
            <MovieCarousel :moviesTitle='moviesCategories.MostPopularMovies' :movies="popularMovies" />
            <MovieCarousel :moviesTitle='moviesCategories.MostPopularTVs' :movies="popularTvMovies" />
        </div>
        <div v-else>
            <LoaderVue/>
        </div>
    </AppLayoutVue>
</template>

<style scoped>
.introSection {
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;
}
</style>