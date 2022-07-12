<template>
  <section>
    <div class="container">
      <div class="flex">
        <div class="card" v-for="element in thisFilmsArray" :key="element.id">
          <div class="card-image">
            <img :src="`https:image.tmdb.org/t/p/w342${element.poster_path}`" alt="">
          </div>
          <div class="card-info">
            <h3>Title: {{element.title}}</h3>
            <h4>Original Title:{{element.original_title}}</h4>
            <div class="original-lang">
              <img class="flag" :src="displayFlagImg(element.original_language)" :alt="element.original_language">
            </div>
            <div class="vote">
              <span>Vote: {{element.vote_average}}</span>
            </div>
          </div>
        </div>
        <!-- <TvSeriesCardComponent v-for="element in thisFilmsArray" :key="element.id" :thisSeriesObject="element"/> -->
        <TvSeriesCardComponent v-for="element in thisSeriesArray" :key="element.id" :thisSeriesObject="element"/>
      </div>
    </div>
  </section>
</template>

<script>
// *IMPORTS
import FilmCardComponent from "./ ";
import TvSeriesCardComponent from "./TvSeriesCardComponent.vue";

export default {
  name: "MainFirstSectionComponent",
  components: {
    FilmCardComponent,
    TvSeriesCardComponent,
  },
  props: {
    thisFilmsArray: Array,
    thisSeriesArray: Array,
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
.flex {
  gap: 1.2rem;
  flex-wrap: wrap;
}
// .card-image > img {
//   aspect-ratio: 2/3;
//   object-fit: cover;
// }
// .original-lang .flag {
//   width: 30px;
//   border: 1px solid black;
// }
</style>