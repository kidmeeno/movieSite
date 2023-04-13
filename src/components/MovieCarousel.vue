<template>
    <div class="carouselWrapper">
        <div class="carouselTitle">
            <h3>{{moviesTitle}}</h3>
        </div>
        <div class="owl-carousel">
            <div class="item" v-for="(movie, index) in movies" :key="index">
                <router-link :to="{ path: '/movie', query: movie }">
                    <img class="movieImage" :src="movie.image?movie.image:'https://via.placeholder.com/150x350'" :alt="movie.title">
                    <p class="movieTitle">{{movie.title}}</p>
                    <p class="movieYear">{{movie.year||'N/A'}}</p>
                </router-link>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"MovieCarousel",
    props: {
        movies: Array,
        moviesTitle: String,
    },

    mounted() {
        $('.owl-carousel').owlCarousel({
            nav: true,
            navText: ['&#10688;', '&#x29C1;'],
            responsive: {
                0: {
                    items: 2,
                },
                600: {
                    items: 3
                },
                1024: {
                    items: 4,
                },
                1440: {
                    items: 6,
                }
            },
        });
    }
};
</script>

<style scoped>
.carouselTitle {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 2rem;
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 28px;
    color: #FDFDFD;
    margin-bottom: 24px;
}

.carouselWrapper {
    position: relative;
}

.movieImage {
    height: 286px;
    margin-bottom: 16px;
    /* width: 219px; */
}

.movieTitle {
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 24px;
    color: #FFFFFF;
    margin-bottom: 8px;
}

.movieYear {
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 20px;
    color: #E0E3E8;
}
</style>
