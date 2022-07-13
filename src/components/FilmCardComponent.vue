<template>
  <div class="card">
    <div class="card-image">
      <img v-if="thisFilm.poster_path !== null" :src="`https:image.tmdb.org/t/p/w342${thisFilm.poster_path}`" :alt="thisFilm.title">
      <img v-else src="../assets/img/image-not-found-3.png" :alt="thisFilm.title">
    </div>
    <div class="card-info">
      <div class="title">
        <span>
          <strong>Title: </strong>
          {{thisFilm.title}}
        </span>
      </div>
      <div v-if="thisFilm.original_title !== thisFilm.title" class="original-title">
        <span>
          <strong>Original Title: </strong>
          {{thisFilm.original_title}}
        </span>
      </div>
      <div class="vote">
        <span v-for="(element, index) in 5" :key="index" class="star" :class="{'full-star': (index + 1) <= voteConverter(thisFilm.vote_average)}">
          <i class="fa-solid fa-star"></i>
        </span>
      </div>
      <div v-if="thisFilm.overview !== ''" class="plot">
        <p>
          <strong>Overview: </strong>
          {{thisFilm.overview}}
        </p>
      </div>
    </div>
    <div class="original-lang">
      <img class="flag" :src="displayFlagImg(thisFilm.original_language)" :alt="thisFilm.original_language">
    </div>
  </div>
</template>

<script>
export default {
  name: "FilmCardComponent",
  props: {
    thisFilm: Object,
  },
  data() {
    return {
      flagPath: "https://countryflagsapi.com/svg/",
      roundedVote: null,
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
    }
  },
  mounted() {
    
  }
}
</script>

<style lang="scss" scoped>
</style>