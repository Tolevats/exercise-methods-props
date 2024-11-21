<template>
  <div class="user-welcome">
    <!-- <div class="user-welcome"> -->
      <!-- botón inicial para pedir datos a usuario -->
      <button @click="getUserData" class="user-btn">Ingresa tus datos</button>
    <!-- </div> -->
    <!-- mostrar mensaje de bienvenida -->
    <div v-if="firstName && lastName" class="welcome-card">
      <h1>¡Bienvenid@ {{ firstName }} {{ lastName }}!</h1>
      <p>Aquí podrás encontrar información de películas de animé del Studio Ghibli.</p>
      <button @click="clearData" class="clear-btn">Limpiar información</button>
    </div>
    <!-- input select para elegir una película -->
    <div v-if="firstName && lastName" class="movie-select-card">
      <h2>A continuación la lista de películas:</h2>
      <select id="movies" v-model="selectedFilm">
        <option disabled value="">Selecciona el film que deseas consultar</option>
        <option v-for="film in movies" :key="film.id" :value="film">
          {{ film.title }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
    name: 'UserWelcome',
    props: {
      movies: {
        type: Array,
        required: true,
      },
    },
    data() {
        return {
            firstName: "",
            lastName: "",
            selectedFilm: "", // almacena el filme seleccionado
        };
    },
    //computed: {},
    methods: {
      getUserData() {
        this.firstName = prompt("Ingresa tu nombre:");
        this.lastName = prompt("Ingresa tu apellido:");
        if (this.firstName && this.lastName) {
            this.$emit("loadMovies"); // Emite un evento para cargar las películas
        }    
      },
      clearData() {
        this.firstName = "";
        this.lastName = "";
        this.selectedFilm = "";
        this.$emit("clearData");
      },
    },
    watch: {
      // observa cambios en el filme seleccionado
      selectedFilm(newFilm) {
        if (newFilm) {
            this.$emit("showFilm", newFilm); // emite el evento automáticamente
        }
      },
    },
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
};
</script>

<style scoped>
.user-welcome {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.user-btn {
  margin: 50px 0;
  padding: 10px 20px;
  font-size: 16px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
.user-btn:hover {
  background-color: #369671;
}
.welcome-card {
  margin: auto;
  padding: 20px;
  text-align: center;
  width: 100%;
  background-color: #f5f5f5;
}
.movie-select-card {
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
  width: 95%;
  text-align: left;
}
.movie-select-card h2 {
  margin-bottom: 10px;
  font-size: 18px;
}
.movie-select-card select {
  margin: 0 20px;
  width: 98%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
}
.clear-btn {
  background-color: #42b983;
  border: none;
  color: white;
  padding: 10px 20px;
  margin-top: 10px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
}
.clear-btn:hover {
  background-color: #369671;
}
</style>