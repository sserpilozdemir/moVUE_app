<template>
  <div class="container" style="margin-top: 94px">
    <section id="favorites" class="bg-dark" v-if="favorites.length > 0">
      <div class="movies-header">
        <h2 class="bg-danger">My Fav Movie List💃🏾 </h2>
      </div>
      <div>
        <div class="col-lg-4 p-5" v-for="fav in favorites" :key="fav.id">
          <div class="card bg-light">
            <img
              class="boxx"
              height="300"
              :src="fav.poster"
              :alt="fav.title"
            />
            <div class="card-body text-dark">
              <h4>{{ fav.title }}</h4>
              <p>{{ fav.description }}</p>
              <div class="row">
                <button style="margin-bottom: 10px"
                  @click="deleteFromFavorites(fav.id)"
                  class="btn btn-outline-dark"
                >
                 <i class="fas fa-heart-broken text-danger"></i>
                </button>
                <a  :href="fav.imdbLink" target="_blank" type="button" id="imbdb-btn" class="btn btn-warning">
                  IMDB
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
   
    <section id="emptyList" v-if="!favorites.length > 0">
      <div class="container" style="margin: 300px auto">
        <h2 class="display-2 text-center">
          There is not any movies here..
        </h2>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      favorites: [],
    };
  },
  methods: {
    deleteFromFavorites(filmID) {
      const deleteQuestion = confirm("Would you like to delete this movie your favorite list ?");
      if (deleteQuestion) {
        axios
          .delete(`http://localhost:3000/movies/${filmID}`)
          .then((delete_response) => {
            this.favorites = this.favorites.filter((i) => i.id != filmID);
          });
      }
    },
  },
  created() {
    console.log(this.favorites);
    axios.get("http://localhost:3000/movies").then((get_response) => {
      console.log(get_response);
      this.favorites = get_response.data;
    });
  },
};
</script>
<style>
boxx{

  background-color: green;
  opacity: 0.3;
}

</style>