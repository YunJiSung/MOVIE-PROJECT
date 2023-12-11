<template>
    <div class="movie-layout">
        <!-- 영화 상세 정보 및 배우 사진 목록 -->
        <div class="movie-details">
            <h2></h2>
            <p></p>
            <div class="cast-container">
                <h3></h3>
                <div class="cast-row1">
                    <div class="cast-item1" v-for="(cast, key) in movieCredits.slice(0, 10)" :key="key">
                        <div class="cast-info1">
                            <img :src="'https://image.tmdb.org/t/p/w500' + cast.profile_path" v-if="cast.profile_path">
                            <p>{{ cast.name }}</p>
                            <p>{{ cast.character }}</p>
                        </div>
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
    display: flex;
    justify-content: center;
    /* 중앙 정렬 */
    margin-top: 20px;
    flex-wrap: wrap;
    /* 요소들이 화면 너비를 넘어갈 경우 줄바꿈 */
}

.cast-row1 {
    display: flex;
    justify-content: center;
    /* 중앙 정렬 */
    gap: 20px;
    /* 배우 사진 사이 간격 */
}

.cast-item1 {
    display: flex;
    flex-direction: column;
    /* 세로 정렬 */
    align-items: center;
    /* 가운데 정렬 */
    width: 150px;
    /* 배우 사진 및 텍스트 영역의 폭 */
    cursor: pointer;
    /* 마우스 호버시 포인터 변경 */
    transition: transform 0.3s ease;
    /* 부드러운 변형 효과 */
}

.cast-item1:hover {
    transform: scale(1.1);
    /* 호버시 약간 확대 */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    /* 호버시 그림자 효과 */
}

.cast-item1 img {
    width: 100%;
    /* 이미지 너비를 컨테이너에 맞춤 */
    height: auto;
    /* 이미지 높이를 자동으로 설정 */
    border-radius: 10px;
    /* 이미지 모서리 둥글게 */
    margin-bottom: 10px;
    /* 이미지와 텍스트 사이 간격 */
}

.cast-info1 p {
    margin: 5px 0;
    /* 텍스트 상하 간격 */
    font-size: 1em;
    /* 텍스트 크기 */
    text-align: center;
    /* 텍스트 중앙 정렬 */
}


/* .cast-container {
    margin-top: 20px;

}

.cast-row {
    display: flex;
    
    gap: 10px;

}

.cast-item img {
    width: auto;

    height: 100px;

    border-radius: 10px;

    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

} */
</style>
  