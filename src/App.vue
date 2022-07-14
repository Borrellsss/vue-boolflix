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
  
        axios.get(this.axiosMoviesUrl).then((response) => {
          // !DEBUG
          // console.log(response.data);
  
          this.moviesArray = response.data.results;
          // !DEBUG
          // console.log(this.moviesArray);
        });
        axios.get(this.axiosSeriesUrl).then((response) => {
          // !DEBUG
          // console.log(response.data);

          this.seriesArray = response.data.results;
          // !DEBUG
          // console.log(this.seriesArray);
        });
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
  
        axios.get(this.axiosMoviesGenreUrl).then((response) => {
          // !DEBUG
          console.log(response.data);
  
          this.moviesArray = response.data.results;
          // !DEBUG
          // console.log(this.moviesArray);
        });
        axios.get(this.axiosSeriesGenreUrl).then((response) => {
          // !DEBUG
          // console.log(response.data);

          this.seriesArray = response.data.results;
          // !DEBUG
          // console.log(this.seriesArray);
        });
      }
    },
    getHomePage() {
      this.axiosMoviesUrl = `https://api.themoviedb.org/3/movie/popular${this.apiKey}${this.langKey}&page=1`;
      // !DEBUG
      // console.log(this.axiosMoviesUrl);

      this.axiosSeriesUrl = `https://api.themoviedb.org/3/tv/popular${this.apiKey}${this.langKey}&page=1`;
      // !DEBUG
      // console.log(this.axiosSeriesUrl);

      axios.get(this.axiosMoviesUrl).then((response) => {
        // !DEBUG
        // console.log(response.data);

        this.moviesArray = response.data.results;
        // !DEBUG
        // console.log(this.moviesArray);
      });
      axios.get(this.axiosSeriesUrl).then((response) => {
        // !DEBUG
        // console.log(response.data);

        this.seriesArray = response.data.results;
        // !DEBUG
        // console.log(this.seriesArray);
      });
    }
  },
  mounted() {
    this.getHomePage()
  }
}
</script>

<style lang="scss">
// *IMPORTS
@import "./style/common.scss";
</style>