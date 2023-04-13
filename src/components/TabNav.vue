<template>
    <div class="wrapper">
        <div class="tabs mb-4">
            <div class="tab" :class="{ 'active': activeTab === 'tab1' }" @click="activeTab = 'tab1'">
                Cast
            </div>
            <div class="tab space" :class="{ 'active': activeTab === 'tab2' }" @click="activeTab = 'tab2'">
                Recommended
            </div>
        </div>
        <div>
            <div v-if="activeTab === 'tab1'">
                <div class="row">
                    <div class="col-6 my-3" v-for="(cast, index) in casts" :key="index">
                        <div class="item">
                            <img class="movieImage" :src="cast.image?cast.image:'https://via.placeholder.com/150x350'" :alt="cast.name">
                            <p class="movieTitle">{{cast.name}}</p>
                            <p class="movieYear">{{cast.asCharacter||'N/A'}}</p>
                        </div>
                    </div>
                </div>
            </div>
            <div v-if="activeTab === 'tab2'">
                <div class="row">
                    <div class="col-6 my-3" v-for="(movie, index) in movies" :key="index">
                        <div class="item">
                            <img class="movieImage" :src="movie.image?movie.image:'https://via.placeholder.com/150x350'" :alt="movie.title">
                            <p class="movieTitle">{{movie.title}}</p>
                            <p class="movieYear">{{movie.year||'N/A'}}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "TabNav",
    data() {
        return {
            activeTab: 'tab1',
        };
    },
    props: {
        casts: Array,
        movies: Array,
    },
};
</script>

<style scoped>
.tabs {
    display: flex;
}

.space {
    margin-left: 16px;
}

.wrapper {
    max-width: 1280px;
    margin: 24px auto;
    padding: 0 2rem;
}

.tab {
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 20px;
    text-align: center;
    color: #C3C5CA;
    padding: 8px;
}

.tab.active {
    font-weight: 400;
    font-size: 15px;
    line-height: 20px;
    text-align: center;
    color: #FDFDFD;
    border-radius: 4px 4px 0px 0px;
    border-bottom: 2px solid #98B6FF;
}

.movieImage {
    width: 100%;
    margin-bottom: 16px;
}

.movieTitle {
    font-weight: 600;
    font-size: 17px;
    line-height: 24px;
    color: #FFFFFF;
}

.movieTitle {
    font-weight: 400;
    font-size: 13px;
    line-height: 20px;
    text-align: center;
    color: #E0E3E8;
}
</style>
