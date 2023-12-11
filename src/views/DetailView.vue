<template>
    <header id="header" role="banner">
        <div class="header__inner">
            <div class="header__nav">
                <h1><a href="/">Movie Star</a></h1>
                <nav>
                    <ul>
                        <li><a herf=""></a></li>
                        <li><a herf=""></a></li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>
    <main id="main">
        <DetailIntro v-if="movieBasic && movieCredits" :movieBasic="movieBasic" :movieCredits="movieCredits" />
        <DetailInfo v-if="movieInfo" :movieInfo="movieInfo" />
        <DetailReview v-if="movieReview" :movieReview="movieReview" />
        <DetailCredits v-if="movieCredits" :movieCredits="movieCredits" />
    </main>
</template>

<script>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axios from 'axios';

import DetailIntro from "../components/detail/DetailIntro.vue";
import DetailInfo from "../components/detail/DetailInfo.vue";
import DetailReview from "../components/detail/DetailReview.vue";
import DetailCredits from "../components/detail/DetailCredits.vue";

export default {
    name: "MovieDetailPage",

    components: {
        DetailIntro,
        DetailInfo,
        DetailReview,
        DetailCredits,

    },

    setup() {
        const movieBasic = ref(null);
        const movieInfo = ref(null);
        const movieReview = ref(null);
        const movieCredits = ref([]);

        const route = useRoute();

        onMounted(async () => {
            const movieId = route.params.movieId;
            const apiKey = import.meta.env.VITE_API_KEY;
            const language = "ko-KR";

            try {
                const resMovieBasic = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`);
                movieBasic.value = resMovieBasic.data;
                console.log(movieBasic)

                const resMovieInfo = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`);
                movieBasic.value = resMovieBasic.data;

                const resMovieReview = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`);
                movieBasic.value = resMovieBasic.data;


                const resMovieCredits = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/credits?language=${language}&api_key=${apiKey}`);
                movieCredits.value = resMovieCredits.data.cast; // 출연진 데이터 할당


            } catch (err) {
                console.log(err)
            }
        });

        return { movieBasic, movieInfo, movieReview, movieCredits };
    }
}
</script>



<style lang="scss">
.header__inner {
    justify-content: space-between;
    align-items: center;
    padding: 1rem;


    .header__nav {
        display: flex;
        justify-content: space-between;
        align-items: center;

        h1 {
            font-size: 24px;
            color: var(--black);
            font-family: '';
            padding: 5px 1rem;
            margin: 20px 10px;
            border: 1px solid var(--black);
            display: inline-block;
            text-transform: uppercase;
        }

        nav {
            li {
                display: inline;

                a {
                    display: inline-block;
                    padding: 10px;
                }
            }
        }
    }

}

.detail__intro {
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;
    padding: 30px;

    &::before {
        content: '';
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        backdrop-filter: blur(10px);
        z-index: 1;
    }

    .container {
        display: flex;
        justify-content: space-between;
        position: relative;
        z-index: 10;

        .left {
            width: 350px;

        }

        .right {
            width: calc(100% - 390px);

            h2 {
                font-size: 30px;
                margin-bottom: 10px;
            }

            p {
                margin-bottom: 10px;
            }

            .desc {
                margin-bottom: 10px;
            }

            .cast-item {

                display: flex; // 추가된 스타일
                gap: 10px; // 추가된 스타일

                img {
                    width: 100px;
                    height: auto;
                    border-radius: 5px;
                    margin: 20px;

                }


            }
        }

    }
}
</style>