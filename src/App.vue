<template>
  <div id="app">
    <!-- componente para manejar bienvenida y selección de películas -->
    <UserWelcome
      :movies="movies"
      @showFilm="showFilm"
      @clearData="clearData"
      @loadMovies="loadMovies"
    />

    <!-- Componente para mostrar detalles de la película -->
    <FilmsList :film="selectedFilm" />
  </div>
</template>

<script>
import UserWelcome from "./components/UserWelcome.vue";
import FilmsList from "./components/FilmsList.vue";

export default {
  name: 'App',
  components: {
    UserWelcome,
    FilmsList,
  },
  data() {
    return {
      movies: [],
      selectedFilm: null, // Almacena la película seleccionada
    };
  },
  methods: {
    async loadMovies() {
      try {
        const response = await fetch("https://ghibliapi.vercel.app/films");
        const data = await response.json();
        this.movies = data.map((film) => ({
          id: film.id,
          title: film.title,
          original_title_romanised: film.original_title_romanised,
          director: film.director,
          running_time: film.running_time,
          description: film.description,
          image: film.image,
        }));
      } catch (error) {
        console.error("Error al cargar las películas:", error);
      }
    },
    showFilm(film) {
      this.selectedFilm = film;
    },
    clearData() {
      this.movies = [];
      this.selectedFilm = null;
    },
  },
  created() {
    this.loadMovies();
  },
};
</script>

<style>
#app {
  box-sizing: border-box;
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: lighter;
  text-align: center;
  /*min-height: 100vh; /* 100vh = Full height of viewport */
}
</style>
