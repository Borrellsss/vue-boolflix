<template>
  <div class="card" @mouseenter="getCast(thisElement)">
    <div class="card-image">
      <img v-if="thisElement.poster_path !== null" :src="`https:image.tmdb.org/t/p/w500${thisElement.poster_path}`" :alt="thisElement.title">
      <img v-else src="../assets/img/image-not-found-3.png" :alt="thisElement.title">
    </div>
    <div class="card-info flex">
      <div class="title">
        <span>
          <strong>Title: </strong>
          {{thisElement.title ? thisElement.title : thisElement.name}}
        </span>
      </div>
      <div v-if="thisElement.original_title !== thisElement.title || thisElement.original_name !== thisElement.name" class="original-title">
        <span>
          <strong>Original Title: </strong>
          {{thisElement.original_title ? thisElement.original_title : thisElement.original_name}}
        </span>
      </div>
      <div class="vote">
        <span v-for="(element, index) in 5" :key="index" class="star" :class="{'full-star': (index + 1) <= voteConverter(thisElement.vote_average)}">
          <i class="fa-solid fa-star"></i>
        </span>
      </div>
      <div v-if="castArray.length > 0" class="cast">
        <strong>Cast: </strong>
        <span v-for="(actor, index) in castArray" :key="index">
          {{`${actor.name}${castArray[index] !== castArray[castArray.length - 1] ? "," : "..."}`}}
        </span>
      </div>
      <div v-hscroll v-if="thisElement.overview !== ''" class="plot">
        <p>
          <strong>Overview: </strong>
          {{thisElement.overview}}
        </p>
      </div>
    </div>
    <div class="original-lang">
      <img class="flag" :src="displayFlagImg(thisElement.original_language)" :alt="thisElement.original_language">
    </div>
  </div>
</template>

<script>
// *IMPORTS
import axios from "axios";

export default {
  name: "CardComponent",
  props: {
    thisElement: Object,
  },
  data() {
    return {
      apiKey: "?api_key=f1240ec31fc689a8980fbeb47322e5ec",
      langKey: "&language=en-US",
      flagPath: "https://countryflagsapi.com/svg/",
      roundedVote: null,
      castArray: [],
      castUrl: "",
    }
  },
  methods: {
    displayFlagImg(lang) {
      if(lang === "en") {
        lang = "us";
      } else if (lang === "ja") {
        lang = "jp";
      } else if (lang === "hi") {
        lang = "in";
      } else if (lang === "cs") {
        lang = "cz";
      } else if (lang === "ko") {
        lang = "kr";
      } else if (lang === "sv") {
        lang = "ch";
      } else if (lang === "fa") {
        lang = "ir";
      } else if (lang === "zh") {
        lang = "cn";
      } else if (lang === "he") {
        lang = "il";
      } else if (lang === "te") {
        lang = "in";
      } else if (lang === "ur") {
        lang = "pk";
      } else if (lang === "sq") {
        lang = "al";
      } else if (lang === "da") {
        lang = "dk";
      } else {
        lang
      }
      return this.flagPath + lang;
    },
    voteConverter(vote) {
      this.roundedVote = vote / 2;
      return Math.round(this.roundedVote);
    },
    getCast(element) {
      const movieCastUrl = `https://api.themoviedb.org/3/movie/${element.id}/credits${this.apiKey}${this.langKey}`;
      const tvCastUrl = `https://api.themoviedb.org/3/tv/${element.id}/credits${this.apiKey}${this.langKey}`;

      if(element.msIsMovie) {
        this.castUrl = movieCastUrl;
      } else {
        this.castUrl = tvCastUrl;
      }

      axios.get(this.castUrl).then((response) => {
        // !DEBUG
        // console.log(response.data.cast.splice(0, 5));

        this.castArray = response.data.cast.splice(0, 5);
        // !DEBUG
        console.log(this.castArray);
      });
    },
  },
}
</script>

<style lang="scss" scoped>
</style>