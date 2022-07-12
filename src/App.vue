<template>
  <div id="app">
    <HeaderComponent @axiosFilmsCall="getFilmsArray" @axiosSeriesCall="getSeriesArray"/>
    <main>
      <MainFirstSectionComponent :thisFilmsArray="filmsArray" :thisSeriesArray="seriesArray"/>
    </main>
  </div>
</template>

<script>
import axios from "axios";
import HeaderComponent from "./components/HeaderComponent.vue";
import MainFirstSectionComponent from "./components/MainFirstSectionComponent.vue";

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainFirstSectionComponent,
  },
  data() {
    return {
      filmTitle: "",
      seriesTitle: "",
      axiosFilmsUrl: "",
      axiosSeriesUrl: "",
      filmsArray: [],
      seriesArray: [],
    }
  },
  methods: {
    getFilmsArray(title) {
      this.filmTitle = title.split(" ").join("+");
      // !DEBUG
      // console.log(this.filmTitle);

      this.axiosFilmsUrl = `https://api.themoviedb.org/3/search/movie?api_key=f1240ec31fc689a8980fbeb47322e5ec&language=it-IT&query=${this.filmTitle}`;
      // !DEBUG
      // console.log(this.axiosFilmsUrl);

      axios.get(this.axiosFilmsUrl).then((response) => {
        // !DEBUG
        // console.log(response.data);

        this.filmsArray = response.data.results;
        // !DEBUG
        console.log(this.filmsArray);
      });
    },
    getSeriesArray(title) {
      this.seriesTitle = title.split(" ").join("+");
      // !DEBUG
      console.log(this.seriesTitle);

      this.axiosSeriesUrl = `https://api.themoviedb.org/3/search/tv?api_key=f1240ec31fc689a8980fbeb47322e5ec&language=it-IT&query=${this.seriesTitle}`;
      // !DEBUG
      console.log(this.axiosSeriesUrl);

      axios.get(this.axiosSeriesUrl).then((response) => {
        // !DEBUG
        console.log(response.data);

        this.seriesArray = response.data.results;
        // !DEBUG
        console.log(this.seriesArray);
      });
    }
  },
}
</script>

<style lang="scss">
// *IMPORTS
@import "./style/common.scss";
</style>
