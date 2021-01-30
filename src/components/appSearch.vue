<template>
  <div>
    <div>      
      <p>
         <font size = "3">
         <marquee align="bottom" width = "1459" direction="left">
         <font color = "Teal" size ="5">
          <strong>Please write a film name which you want to be search in database.</strong>
          </font>
          </marquee>
          </font>
      </p>
      <form action="get">
        <input
          type="text"
          id="search-box"
          class="box-new"
          placeholder="Please write a film name.."
          v-model="filmName"
          @keypress.enter="searchFilm"
        />
        <button
          @click="searchFilm"
          type="button"
          class="button"
        >
          Search
          <i class="fas fa-search"></i>
        </button>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      filmName: "",
    };
  },
  methods: {
    searchFilm() {      
      this.$emit("search-film-event", this.filmName);
      console.log(this.filmName);
      this.filmName = "";      
    },
  },
};
</script>
