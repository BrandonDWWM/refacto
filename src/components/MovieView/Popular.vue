<template>
  <div class="head">
    <div class="title">Popular</div>
    <div class="more">More</div>
  </div>
  <div class="slider-container">
    <div class="slider" ref="slider">
      <div v-for="movie in popularMovies">
        <MovieCard
          :title="movie.title"
          :image="movie.image"
          :score="movie.rank"
          :id="movie.id"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import MovieCard from './MovieCard.vue';
const popularMovies = ref([]);

onMounted(() => {
  fetch('datas/popular.json')
    .then(response => response.json())
    .then(data => {
      popularMovies.value = data.popular;
    })
    .catch(error => console.error('Erreur lors du chargement du JSON:', error));
});
</script>

<style scoped>
  .head {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    width: 100%;
    padding: 35px 15px 0 15px;
  }

  .title {
    font-size: 28px;
    font-weight: 900;
  }

  .more {
    color: rgb(104, 147, 187);
  }

  .slider-container {
    padding: 0 16px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
  }

  .slider {
    display: flex;
    flex-wrap: nowrap;
    gap: 16px;
    padding: 0; 
    overflow-x: auto;
    scroll-behavior: smooth;
    margin: 0; 
  }
</style>