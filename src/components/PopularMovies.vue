<template>
  <div
    v-for="(movie, id) in moviesData"
    :key="id"
    class="flex flex-shrink-0 justify-center items-center w-1/2 max-w-sm mx-auto my-8"
  >
    <div
      :style="{
        backgroundImage: `url(${baseImgUrl}/w500${movie.backdrop_path})`
      }"
      class="bg-gray-300 h-64 w-full rounded-lg shadow-md bg-cover bg-center"
    ></div>
  </div>
</template>

<script>
import { ref } from "vue";
import MovieService from "../../Services/MovieService.js";
export default {
  setup() {
    const baseImgUrl = ref("https://image.tmdb.org/t/p");
    const moviesData = ref([]);
    // eslint-disable-next-line no-unused-vars
    async function loadData() {
      try {
        const moviedata = await MovieService.getPopularMovies();
        moviesData.value = moviedata.data.results;
        console.log(moviesData.value);
      } catch (err) {
        console.log(err);
      }
    }
    loadData();
    return { baseImgUrl, moviesData };
  }
};
</script>
