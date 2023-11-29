<template>
    <header id="header" role="banner">
        <div class="header__inner">
            <div class="header__nav">
                <h1>Movie Site</h1>
                <nav>
                    <ul>
                        <li><a herf=""></a>추천 영화 Top10</li>
                        <li><a herf=""></a>코딩 영화 Top10</li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>
    <main id="main">
        <div class="detail__intro"
            :style="{ backgroundImage: 'url(https://image.tmdb.org/t/p/w500/kjQBrc00fB2RjHZB3PGR4w9ibpz.jpg)' }">
            <div class="container">
                <div class="left play icon">
                    <img :src="'https://image.tmdb.org/t/p/w500' + movieInfo.poster_path" :alt="movieInfo.title">
                </div>
                <div class="right">
                    <h2>{{ movieInfo.title }}</h2>
                    <p class="desc">{{ movieInfo.overview }}</p>
                    <p class="date">개봉일: {{ movieInfo.release_date }}</p>
                    <p class="average">평점: {{ movieInfo.vote_average }}</p>

                    <div class="credits" v-if="movieInfo.actors && movieInfo.actors.length > 0">
                        <div v-for="actor in movieInfo.actors.slice(0, 5)" :key="actor.id">
                            <img :src="'https://image.tmdb.org/t/p/w500' + actor.profile_path" :alt="actor.name" />
                        </div>
                    </div>
                    <!-- <div class="credits">
                        <div v-for="actor in movieInfo.actors" :key="actor.id">
                            <img :src="'https://image.tmdb.org/t/p/w500' + actor.profile_path" :alt="actor.name" />
                        </div>
                    </div> -->
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import FooterSection from '../components/section/FooterSection.vue';
import HeaderSection from '../components/section/HeaderSection.vue';
export default {
    setup() {
        const route = useRoute();
        const movieInfo = ref({});
        const movieInfoFetch = (movieId) => {
            const apiKey = import.meta.env.VITE_API_KEY;

            const movieInfoPromise = fetch(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${apiKey}&language=ko-KR`)
                .then((response) => response.json());
            const creditsPromise = fetch(`https://api.themoviedb.org/3/movie/${movieId}/credits?api_key=${apiKey}`)
                .then((response) => response.json());
            Promise.all([movieInfoPromise, creditsPromise])
                .then((results) => {
                    const [movieInfoResult, creditsResult] = results;

                    const mergedMovieInfo = { ...movieInfoResult, actors: creditsResult.cast };

                    movieInfo.value = mergedMovieInfo;

                    console.log(movieInfo.value);
                })
                .catch((err) => {
                    console.log(err);
                });
        };
        onMounted(() => {
            const movieId = route.params.movieId;
            movieInfoFetch(movieId);
        });
        return {
            movieInfo,
        };
    },
    components: { FooterSection, HeaderSection }
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
                margin-bottom: 5px;
            }

            .desc {
                margin-bottom: 10px;
            }

            .credits {
                display: flex; // 추가된 스타일
                gap: 10px; // 추가된 스타일

                div {
                    flex: 0 0 auto;

                    img {
                        width: 100px;
                        height: auto;
                        border-radius: 5px;
                    }
                }
            }
        }

    }
}
</style>