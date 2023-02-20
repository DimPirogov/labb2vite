<script>
import axios from "axios";

export default {
  created() {
    this.apiCall();
  },
  methods: {
    searchOn(event) {
      if (event) {
        this.searchKey = this.searchOnpage;
        this.apiCall();
        event.preventDefault();
      }
    },
    async apiCall() {
      if (this.searchKey === "") this.searchKey = "game";
      this.loading = true;
      const options = {
        method: "GET",
        url: "https://imdb8.p.rapidapi.com/auto-complete",
        params: { q: this.searchKey },
        headers: {
          "X-RapidAPI-Key":
            "c4244b7623msh0c351195a859171p16145ejsn7c442196b92d",
          "X-RapidAPI-Host": "imdb8.p.rapidapi.com",
        },
      };
      try {
        const response = await axios.request(options);
        const moviesList = response.data;
        this.movies = moviesList.d;
      } catch (err) {
        console.log(err);
        this.response = err; //för errors
      } finally {
        this.loading = false; // sätter loading till falsk
      }
    },
  },
  data() {
    return {
      searchOnpage: "",
      searchKey: "",
      loading: false,
      movies: [], // sparas svar här
    };
  },
};
</script>

<template>
  <div class="container">
    <h1>Listing movies</h1>
    <form class="col-lg-6 offset-lg-3">
      <div class="form-group mb-1">
        <input
          type="text"
          class="form-control"
          id="searchMoviesField"
          placeholder="search movie"
          aria-describedby="emailHelp"
          v-model="searchOnpage"
        />
      </div>
      <button @click="searchOn" type="submit" class="btn btn-primary mb-1">
        Search movies
      </button>
    </form>
    <button v-if="loading" class="btn btn-primary" type="button" disabled>
      <span
        class="spinner-border spinner-border-sm"
        role="status"
        aria-hidden="true"
      ></span>
      Loading Movies...
    </button>
    <div v-else>
      <div class="row">
        <div class="col-lg-4" v-for="movie in movies" :key="movie.id">
          <div class="card mb-1" style="width: 16rem">
            <!-- <img :src="movie.i.imageUrl" class="card-img-top" :alt="movie.l" /> -->
            <!-- av någon anledning funkar inte images, trots att det är rätt -->
            <div class="card-body">
              <h5 class="card-title">{{ movie.l }}</h5>
              <p class="card-text">Ranking: {{ movie.rank }}</p>
              <p class="card-text">Actors: {{ movie.s }}</p>
              <p class="card-text">Year: {{ movie.y }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
