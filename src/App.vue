<script setup>
import MovieList from "./components/MovieList.vue"
</script>

<template>
  <main>
    <div class="Container">
      <h1>TheDruuCinemax</h1>
      <p>Nonton gratiss gak pake bayar!</p>
      <div class="Movie-container">
        <MovieList/>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
.Container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
p{
  margin-bottom: 20px;
}

.Movie-container {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 20px;
}
</style>
