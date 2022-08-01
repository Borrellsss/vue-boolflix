<template>
  <div id="app">
    <HeaderComponent @axiosCall="getApiCall" @axiosGenresCall="getApiGenresCall"/>
    <main>
      <FirstSectionComponent :thisMoviesArray="moviesArray" :thisSeriesArray="seriesArray"/>
    </main>
  </div>
</template>

<script>
// *IMPORTS
import axios from "axios";
import HeaderComponent from "./components/HeaderComponent.vue";
import FirstSectionComponent from "./components/FirstSectionComponent.vue";

export default {
  name: 'App',
  components: {
    HeaderComponent,
    FirstSectionComponent,
  },
  data() {
    return {
      title: "",
      genre: null,
      apiKey: "?api_key=f1240ec31fc689a8980fbeb47322e5ec",
      langKey: "&language=en-US",
      axiosMoviesUrl: "https://api.themoviedb.org/3/search/movie",
      axiosSeriesUrl: "https://api.themoviedb.org/3/search/tv",
      axiosMoviesGenreUrl: "https://api.themoviedb.org/3/discover/movie",
      axiosSeriesGenreUrl: "https://api.themoviedb.org/3/discover/tv",
      axiosMoviesTopRatedUrl: "",
      axiosSeriesTopRatedUrl: "",
      moviesArray: [],
      seriesArray: [],
      homePageArray: ["popular", "top_rated"],
      randomHomeIndex: "",
      randomHomePage: "",
    }
  },
  methods: {
    getApiCall(userInput) {
      this.title = userInput.split(" ").join("+");
      // !DEBUG
      // console.log(this.title);

      if(this.title.length === 0) {
        this.getHomePage();
      } else {
        this.axiosMoviesUrl = "https://api.themoviedb.org/3/search/movie";
        this.axiosMoviesUrl += `${this.apiKey}${this.langKey}&query=${this.title}`;
        // !DEBUG
        // console.log(this.axiosMoviesUrl);

        this.axiosSeriesUrl = "https://api.themoviedb.org/3/search/tv";
        this.axiosSeriesUrl += `${this.apiKey}${this.langKey}&query=${this.title}`;
        // !DEBUG
        // console.log(this.axiosSeriesUrl);
  
        this.axiosMovieAndTVCall(this.axiosMoviesUrl, this.axiosSeriesUrl);
      }
      userInput = "";
    },
    getApiGenresCall(userGenre) {
      this.genre = userGenre;
      // !DEBUG
      // console.log(this.genre);

      if(this.genre === "all") {
        this.getHomePage();
      } else {
        this.axiosMoviesGenreUrl = "https://api.themoviedb.org/3/discover/movie";
        this.axiosMoviesGenreUrl += `${this.apiKey}${this.langKey}&with_genres=${this.genre}`;
        // !DEBUG
        // console.log(this.axiosMoviesGenreUrl);

        this.axiosSeriesGenreUrl = "https://api.themoviedb.org/3/discover/tv";
        this.axiosSeriesGenreUrl += `${this.apiKey}${this.langKey}&with_genres=${this.genre}`;
        // !DEBUG
        // console.log(this.axiosSeriesGenreUrl);
  
        this.axiosMovieAndTVCall(this.axiosMoviesGenreUrl, this.axiosSeriesGenreUrl);
      }
    },
    getHomePage() {
      for(let i = 0; i < this.homePageArray.length; i++) {
        this.randomHomeIndex = this.getRndInteger(0 , this.homePageArray.length);
        this.randomHomePage = this.homePageArray[this.randomHomeIndex];
      }
      // !DEBUG
      // console.log(this.randomHomePage);

      this.axiosMoviesUrl = `https://api.themoviedb.org/3/movie/${this.randomHomePage}${this.apiKey}${this.langKey}&page=1`;
      // !DEBUG
      // console.log(this.axiosMoviesUrl);

      this.axiosSeriesUrl = `https://api.themoviedb.org/3/tv/${this.randomHomePage}${this.apiKey}${this.langKey}&page=1`;
      // !DEBUG
      // console.log(this.axiosSeriesUrl);

      this.axiosMovieAndTVCall(this.axiosMoviesUrl, this.axiosSeriesUrl);
    },
    axiosMovieAndTVCall(movieUrl, tvUrl) {
      axios.get(movieUrl).then((response) => {
        // !DEBUG
        // console.log(response.data);

        this.moviesArray = response.data.results;
        // !DEBUG
        // console.log(this.moviesArray);

        this.moviesArray.forEach((element) => {
          element.msIsMovie = true;
        });
      });

      axios.get(tvUrl).then((response) => {
        // !DEBUG
        // console.log(response.data);
        
        this.seriesArray = response.data.results;
        // !DEBUG
        // console.log(this.seriesArray);

        this.seriesArray.forEach((element) => {
          element.msIsMovie = false;
        });
      });
    },
    getRndInteger(min, max) {
      return Math.floor(Math.random() * (max - min)) + min;
    }
  },
  mounted() {
    this.getHomePage();
  }
}
</script>

<style lang="scss">
// *IMPORTS
@import "./style/common.scss";
</style>