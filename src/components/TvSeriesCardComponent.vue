<template>
  <div class="card">
    <div class="card-image">
      <img v-if="thisSeries.poster_path !== null" :src="`https:image.tmdb.org/t/p/w342${thisSeries.poster_path}`" :alt="thisSeries.name">
      <img v-else src="../assets/img/image-not-found-3.png" :alt="thisSeries.name">
    </div>
    <div class="card-info">
      <div class="title">
        <span>
          <strong>Name: </strong>
          {{thisSeries.name}}
        </span>
      </div>
      <div v-if="thisSeries.original_name !== thisSeries.name" class="original-title">
        <span>
          <strong>Original Name: </strong>
          {{thisSeries.original_name}}
        </span>
      </div>
      <div class="vote">
        <span v-for="(element, index) in 5" :key="index" class="star" :class="{'full-star': (index + 1) <= voteConverter(thisSeries.vote_average)}">
          <i class="fa-solid fa-star"></i>
        </span>
      </div>
      <div v-if="thisSeries.overview !== ''" class="plot">
        <p>
          <strong>Overview: </strong>
          {{thisSeries.overview}}
        </p>
      </div>
    </div>
    <div class="original-lang">
      <img class="flag" :src="displayFlagImg(thisSeries.original_language)" :alt="thisSeries.original_language">
    </div>
  </div>
</template>

<script>
export default {
  name: "TvSeriesCardComponent",
  props: {
    thisSeries: Object,
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