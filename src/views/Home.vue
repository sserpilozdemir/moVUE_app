<template>
    <div>
    <div class="container" style="margin-top: 50px">
      <!--     Film search area -->
      <app-search @search-film-event="getFilmsFromDb"/>
      <app-movie-list :movies="movies"/>
    </div>
  </div>
    
</template>

<script>
import axios from "axios";
import appSearch from "@/components/appSearch";
import appMovieList from "@/components/appMovieList";
export default {
  components: {
    appSearch,
    appMovieList
  },
  data() {
    return {
      movies: [],
    };
  },
  methods: {
    getFilmsFromDb(value) {
      if (value != "") {
        const film = value;
        axios
          .get(`http://www.omdbapi.com/?apikey=7b38c1a8&s=${film}`)
          .then((get_response) => {
            this.movies = get_response.data.Search.map((m) => {
                console.log(m.Title);
              return {
                title: m.Title,
                description: `${m.Year} / ${m.Type}`,
                imdbID: m.imdbID,
                poster:
                  m.Poster === "N/A"
                    ? "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTJnb43MuKReMIG9fvcHJrOAupaJjzKCcEdyw&usqp=CAU"
                    : m.Poster,
                imdbLink: `https://www.imdb.com/title/${m.imdbID}`,
                isExist: false
              };
            });
          });
      }
      console.log(this.movies);
    },
  
  }
};
</script>
