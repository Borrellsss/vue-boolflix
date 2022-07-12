<template>
  <div class="card">
    <div class="card-image">
      <img :src="`https:image.tmdb.org/t/p/w342${thisSeriesObject.poster_path}`" alt="">
    </div>
    <div class="card-info">
      <h3>{{thisSeriesObject.name}}</h3>
      <h4>{{thisSeriesObject.original_name}}</h4>
      <div class="original-lang">
        <img class="flag" :src="displayFlagImg(thisSeriesObject.original_language)" :alt="thisSeriesObject.original_language">
      </div>
      <div class="vote">
        <span>{{thisSeriesObject.vote_average}}</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "TvSeriesCardComponent",
  props: {
    thisSeriesObject: Object,
  },
  data() {
    return {
      flagPath: "https://countryflagsapi.com/svg/",
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
      } else {
        lang
      }

      return this.flagPath + lang;
    },
  },
  mounted() {
    
  }
}
</script>

<style lang="scss" scoped>
</style>