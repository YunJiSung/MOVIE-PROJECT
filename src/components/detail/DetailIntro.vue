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
                        <!-- <p>{{ cast.character }}</p>
                        <p>{{ cast.name }}</p> -->
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

<style>
.cast-row {
    display: flex;
    flex-wrap: wrap;
    /* 여러 배우들을 위해 줄바꿈 허용 */
    gap: 10px;
    /* 배우들 사이의 간격 */
}

.cast-item {
    display: flex;
    flex-direction: column;
    /* 세로 정렬 */
    align-items: center;
    /* 가운데 정렬 */
    width: 100px;
    /* 배우 사진 및 텍스트 영역의 폭 */
}

.cast-item img {
    width: 100%;
    /* 이미지 너비를 컨테이너에 맞춤 */
    height: auto;
    /* 이미지 높이를 자동으로 설정 */
    border-radius: 10px;
    /* 이미지 모서리 둥글게 */
}

.cast-item p {
    margin: 10px 0;
    /* 텍스트 상하 간격 */
    font-size: 0.9em;
    /* 텍스트 크기 */
    text-align: center;
    /* 텍스트 중앙 정렬 */
}

.cast-item p:first-child {
    font-weight: bold;
    /* 캐릭터 이름 강조 */
}
</style>