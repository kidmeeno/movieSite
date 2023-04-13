<template>
    <div class="wrapper">
        <div class="carouselTitle">
            <h3>{{title}}</h3>
        </div>
        <div class="owl-carousel">
            <div class="item" v-for="(cast, index) in casts" :key="index">
                <img class="castImage" :src="cast.image?cast.image:'https://via.placeholder.com/150x350'" :alt="cast.id">
                <p class="castTitle">{{cast.name}}</p>
                <p class="castAsCharacter">{{cast.asCharacter}}</p>
            </div>
        </div>
    </div>
</template>

<script>
import 'owl.carousel/dist/assets/owl.carousel.css';
import 'owl.carousel';

export default {
    name:'UserCarousel',
    props: {
        casts: Array,
        title: String
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
            }
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

.wrapper {
    position: relative;
}

.castImage {
    height: 286px;
    margin-bottom: 16px;
}

.castTitle {
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 24px;
    color: #FFFFFF;
    margin-bottom: 8px;
}

.castAsCharacter {
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 20px;
    color: #E0E3E8;
}
</style>
