<template>
    <div class="movie-layout">
        <!-- 영화 상세 정보 및 배우 사진 목록 -->
        <div class="movie-details">
            <h2>"The Creator"</h2>
            <p>영화에 대한 설명...</p>
            <div class="cast-container">
                <h3>주연 배우</h3>
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
        movieCredits: {
            type: Array,
            required: true,
        },
        // 포스터 이미지 경로는 prop으로 받거나 data 속성에서 정의할 수 있습니다.
        posterPath: {
            type: String,
            required: true,
        }
    },
}
</script>
  
<style>
.movie-layout {
    display: flex;
    align-items: flex-start;
    /* 상단 정렬 */
    gap: 20px;
    /* 요소들 사이 간격 */
}

.movie-poster img {
    max-width: 300px;
    /* 포스터 최대 너비 */
    border-radius: 10px;
    /* 둥근 모서리 */
}

.movie-details {
    flex-grow: 1;
}

.cast-container {
    margin-top: 20px;
    /* 배우 사진 목록 위 간격 */
}

.cast-row {
    display: flex;
    /* 가로 정렬 */
    gap: 10px;
    /* 배우 사진 사이 간격 */
}

.cast-item img {
    width: auto;
    /* 원본 비율 유지 */
    height: 100px;
    /* 일정한 높이 설정 */
    border-radius: 10px;
    /* 둥근 모서리 */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    /* 그림자 효과 */
}
</style>
  