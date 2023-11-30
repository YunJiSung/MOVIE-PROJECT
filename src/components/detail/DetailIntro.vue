<template>
    <div class="detail__intro"
        :style="{ backgroundImage: 'url(https://image.tmdb.org/t/p/w500/' + movieBasic.backdrop_path + ')' }">
        <div class="container">
            <div class="left play icon">
                <img :src="'https://image.tmdb.org/t/p/w500' + movieBasic.poster_path" :alt="movieBasic.title">
            </div>
            <div class="right">
                <h2>{{ movieBasic.title }}</h2>
                <p class="desc">{{ movieBasic.overview }}</p>
                <p class="date">개봉일: {{ movieBasic.release_date }}</p>
                <p class="average">평점: {{ movieBasic.vote_average }}</p>
                <p>기본 언어: {{ movieBasic.original_language }}</p>
                <p>인기: {{ movieBasic.popularity }}</p>
                <p>개봉일: {{ movieBasic.release_date }}</p>
                <p>상영시간: {{ movieBasic.runtime }}</p>

                <div class="cast-row">
                    <div class="cast-item" v-for="(cast, key) in movieCredits.slice(0, 5)" :key="key">
                        <img :src="'https://image.tmdb.org/t/p/w500' + cast.profile_path" v-if="cast.profile_path">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    props: {
        movieBasic: {
            type: Object,
            required: true,
        },
        movieCredits: {
            type: Object,
            required: true,
        },
    },
}

</script>