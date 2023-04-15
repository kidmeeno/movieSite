<template>
    <div class="MovieDetailWrapper">
        <div class="bgImage">
            <img :src="movieDetails.image" />
        </div>
        <div class="wrapper">
            <section class="introSection row">
                <div class="content col-md-6 p-0">
                    <p class=""><span>Featured</span> | {{movieDetails.year}} | Action, Sci-Fi, Drama</p>
                    <h1 class="mb-2">{{movieDetails.title}}</h1>
                    <div class="d-flex align-items-center mb-3">
                        <img src="../assets/star.svg" />
                        <p class="my-0 mx-1">{{movieDetails.imDbRating||'N/A'}}</p>
                        <div class="ageRatingBox mx-2">{{movieDetails.contentRating||'N/A'}}</div>
                    </div>
                    <p class="mb-4">{{movieDetails?.plot||'We dont have summary on this one. But surely you can tell from the cover it is going to be a fun watch. Have fun! :)'}}</p>
                    <div class="buttonGroup">
                        <button class="watchNowBtn"><img src="../assets/play-circle.svg" class="mx-2"/>Watch now</button>
                        <button v-if="!hideLearnBtn" class="learnMoreBtn"><img src="../assets/info-circle.svg" class="mx-2"/>Learn more</button>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MovieDetailSection',
    props: {
        movieDetails: Object,
        hideLearnBtn: Boolean,
    },
}
</script>

<style scoped>
.introSection {
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;
}

.watchNowBtn {
    background: #3772FF;
    border: none;
    margin-right: 10px;
}

.MovieDetailWrapper {
    position: relative;
}

.bgImage {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    object-fit: cover;
    height: 583px;
}

.bgImage>img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.learnMoreBtn {
    background: #21354A;
    border: none;
}

.wrapper {
    background: linear-gradient(90deg, rgba(27, 31, 50, 0.4) 41.56%, rgba(27, 31, 50, 0) 97.11%);
    width: 100%;
    background-size: cover;
    background-repeat: no-repeat;
    height: 583px;
    padding: 10% 0;
    margin-bottom: 48px;
    position: relative;
}

.content {
    color: #FDFDFD;
}

.content>p {
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;
}

.content>p>span {
    color: #E8BA35;
}

.content>h1 {
    font-style: normal;
    font-weight: 600;
    font-size: 42px;
    line-height: 44px;
}

.ageRatingBox {
    width: 49px;
    height: 28px;
    border: 1px solid #CBD1D8;
    border-radius: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.buttonGroup>button {
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 20px;
    text-align: center;
    color: #FFFFFF;
    padding: 12px 24px;
    border-radius: 6px;
}

@media (max-width: 766px) {
    .wrapper {
        margin-bottom: 0px;
        padding: 105px 0px 121px 0;
        /* height: auto; */
    }
    .bgImage {
        /* height: 449px; */
    }
}
</style>