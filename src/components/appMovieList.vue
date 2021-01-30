<template>
  <section id="movies" v-if="movies.length > 0">
    <div class="movies-header">
            <h2 class="text-center display-15 text-danger">M O V I E S</h2>
    </div>
    <div class="container" style="margin-top: 400px">
      <div class="col-lg-4 p-5" v-for="movie in movies" :key="movie.imbdbID">
        <div class="card bg-secondary">
          <img
            class="card-img-top"
            height="300"
            :src="movie.poster"
            :alt="movie.title"
          />
          <div class="card-body text-light">
            <h4>{{ movie.title }}</h4>
            <p>{{ movie.description }}</p>
            <div class="d-flex flex-column">
              <button
                id="btn-fav"
                type="button"
                class="btn btn-outline-danger"
                style="margin-bottom: 10px"
                @click="addToFavorites(movie)"
              >
                <i class="fas fa-heart"></i>
              </button>
              <a
                :href="movie.imdbLink"
                target="_blank"
                type="button"
                id="imbdb-btn"
                class="btn btn-warning"
              >
                IMDB
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  props: ["movies"],
  data() {
    return {
      favorites: [],
      isExist : false
    };
  },
  methods: {
    addToFavorites(movie) {
      const isExist = this.favorites.filter((x) => x.imdbID === movie.imdbID);

      if (isExist.length > 0) {
        alert("This movie has already exist your favorite movie list!");
      } else {
        axios
          .post("http://localhost:3000/movies", movie)
          .then((add_response) => {
            axios.get("http://localhost:3000/movies").then((get_response) => {
              this.favorites = get_response.data;
            });
          });
      }
    },
  },
  created() {
    axios.get("http://localhost:3000/movies").then((get_response) => {
      this.favorites = get_response.data;
    });
  },
};
</script>
