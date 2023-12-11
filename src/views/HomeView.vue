<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import HeaderSection from '@/components/section/HeaderSection.vue';
import FooterSection from '@/components/section/FooterSection.vue';



const movies = ref([]);
const searchKeyword = ref('');



const fetchMovies = async (category) => {
  let url = 'https://api.themoviedb.org/3/movie/popular';

  switch (category) {
    case 'latest':
      url = 'https://api.themoviedb.org/3/movie/now_playing';
      break;
    case 'popular':
      url = 'https://api.themoviedb.org/3/movie/popular';
      break
    case 'upcoming':
      url = 'https://api.themoviedb.org/3/movie/upcoming';
      break
    case 'top_rated':
      url = 'https://api.themoviedb.org/3/movie/top_rated';
      break
  }

  try {
    const response = await axios.get(url, {
      params: {
        api_key: '411a4542de8350a31fbd318eb41652b8',
        language: 'ko-KR',
        page: '1'
      }
    });

    movies.value = response.data.results;
    console.log(response.data.results);
  } catch (err) {
    console.error(err);
  }
}

const searchMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: '411a4542de8350a31fbd318eb41652b8',
        language: 'ko-KR',
        query: searchKeyword.value,
        page: '1'
      }
    });
    movies.value = response.data.results;
  } catch (err) {
    console.error(err);
  }
}


onMounted(async () => {
  await fetchMovies('latest');
});


</script>

<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="container">
      <div class="movie__inner">

        <section class="movie__search">
          <h2 class="blind">검색하기</h2>
          <input type="search" v-model="searchKeyword" placeholder="검색어를 입력해주세요!" @keyup.enter="serachMovies">
          <button type="submit" @click="serachMovies">검색</button>
        </section>
        <!-- //movie__search -->

        <div class="movie__tag">
          <ul>
            <li><a href="#" @click="fetchMovies('latest')">최신 영화</a></li>
            <li><a href="#" @click="fetchMovies('popular')">인기 영화</a></li>
            <li><a href="#" @click="fetchMovies('upcoming')">개봉 예정</a></li>
            <li><a href="#" @click="fetchMovies('top_rated')">최고 평점</a></li>
          </ul>
        </div>
        <!-- //movie__tag -->

        <section class="movie__cont">
          <h2 class="blind">영화</h2>
          <div class="movie play__icon" v-for="movie in movies" :key="movie.id">
            <a :href="'/detail/' + movie.id">
              <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title">
            </a>
          </div>
        </section>
        <!-- //movie__cont -->

      </div>
    </div>
  </main>
  <FooterSection />
</template>

<script>
import HeaderSection from '@/components/section/HeaderSection.vue';
import FooterSection from '@/components/section/FooterSection.vue';

import MovieSearch from "@/components/contents/MovieSearch.vue";
import MovieTag from "@/components/contents/MovieTag.vue";
import MovieCont from "@/components/contents/MovieCont.vue";

export default {
  name: "MovieHomePage",
  components: {
    HeaderSection,
    FooterSection,
    MovieSearch,
    MovieTag,
    MovieCont
  },
  data() {
    return {
      movies: [],
    }
  },
  methods: {
    async search(query) {
      try {
        const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=411a4542de8350a31fbd318eb41652b8&language:ko-KR&query=${query}`)
        const result = await response.json();
        console.log(result);
      } catch (error) {
        console.log(error)
      }
    },
    async tags(query) {
      try {
        const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=411a4542de8350a31fbd318eb41652b8&language:ko-KR&query=${query}`)
        const result = await response.json();
        console.log(result);
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>


<style lang="scss">
.movie__search {
  display: flex;
  justify-content: center;
  margin: 1rem;

  input {
    border: 1px solid #ddd;
    padding: 0.75rem 1rem;
    width: 100%;
    max-width: 600px; // Limit the width of the input field
    border-radius: 20px; // Rounded corners
    margin-right: 1rem;
  }

  button {
    padding: 0.75rem 1rem;
    background-color: #333; // Dark background for the button
    color: #fff;
    border: none;
    border-radius: 20px;
    cursor: pointer;

    &:hover {
      background-color: darken(#333, 10%);
    }
  }
}

.movie__tag ul {
  display: flex;
  list-style: none;
  padding: 0;
  margin: 1rem 0;

  li a {
    padding: 0.5rem 1rem;
    margin-right: 0.5rem;
    border-radius: 20px;
    transition: background-color 0.3s;

    &:hover {
      background-color: #eee; // Light hover effect
    }
  }
}

.movie__cont {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  padding: 1rem;
}

.movie {
  background-color: #f4f4f4; // Light background for movie cards
  border-radius: 10px; // Rounded corners for cards
  overflow: hidden;

  img {
    width: 100%;
    height: auto;
    display: block;
  }

  &:hover {
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); // Shadow effect on hover
  }
}

// .movie__search {
//   margin: 50px 0 20px;
//   position: relative;

//   input {
//     border: 1px solid var(--black);
//     padding: 1rem 2rem;
//     width: 100%;
//     border-radius: 50px;
//   }

//   button {
//     position: absolute;
//     right: 6px;
//     top: 6px;
//     width: 40px;
//     height: 40px;
//     background-color: var(--black);
//     color: #fff;
//     border-radius: 50%;
//   }
// }

// .movie__tag {
//   ul {
//     display: flex;

//     li {
//       a {
//         border: 1px solid var(--black);
//         padding: 0.5rem 1.3rem;
//         display: inline-block;
//         border-radius: 50px;
//         margin-bottom: 20px;
//         margin-right: 10px;
//         margin-top: 20px;

//         &:hover {
//           background-color: var(--black);
//           color: var(--white);
//         }
//       }
//     }
//   }
// }

// .movie__cont {
//   display: flex;
//   justify-content: space-between;
//   flex-wrap: wrap;

//   .movie {
//     width: 24%;
//     margin-bottom: 1.5%;
//     background-color: #ccc;
//   }
// }
</style>
