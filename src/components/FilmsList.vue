<template>
  <div v-if="film" class="film-card">
    <img :src="film.image" alt="Imagen del anime">
    <h3><strong>{{ film.title }}</strong></h3>
    <h4><strong>Original title:</strong> {{ film.original_title_romanised }}</h4>
    <p><strong>Summary:</strong> {{ film.description }}</p>
    <h5><strong>Director:</strong> {{ film.director }}</h5>
    <h6><strong>Runtime:</strong> {{ film.running_time }} min</h6>
  </div>
</template>

<script>
export default {
    name: 'FilmsList',
    props: {
      film: {
        type: Object,
        default: null,
      },
    },
/*     data: function(){
        return {}
    }, */
    // computed: {},
    //methods: {}
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
};
</script>

<style scoped>
/* Card styles for content */
.film-card {
  margin: 20px auto;
  padding: 16px;
  border: 1px solid #ddd;
  border-radius: 10px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-align: center;
  width: calc(100% - 40px);
}
.film-card img {
  width: 100%;
  object-fit: cover; /* Ensure image scaling */
  margin: 10px 0;
  border: 2px solid #ddd;
  border-radius: 5px;
}
.film-card h3 {
  font-size: 1.2em;
  color: #42b983;
  margin-bottom: 10px;
}
.film-card p {
  margin: 5px 0;
  font-size: 0.9em;
  line-height: 1.5;
}
h3, h4, h5, h6 {
    font-weight: 100;
}
/* Estilos responsivos */
@media (min-width: 768px) {
  .film-card {
    max-width: 800px;
  }

  .film-card h3 {
    font-size: 1.5em;
  }

  .film-card p {
    font-size: 1em;
  }
} 
</style>