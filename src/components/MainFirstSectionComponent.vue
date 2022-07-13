<template>
  <section>
    <div class="container">
      <div v-if="thisFilmsArray.length > 0" class="films">
        <h2>Movies</h2>
        <div v-hscroll class="flex">
            <FilmCardComponent v-for="element in thisFilmsArray" :key="element.id" :thisFilm="element"/>
        </div>
      </div>
      <div v-else class="films not-found">
        <h2>Movie not Found</h2>
      </div>
      <div v-if="thisSeriesArray.length > 0" class="tv-series">
        <h2>TV Series</h2>
        <div v-hscroll class="flex">
          <TvSeriesCardComponent v-for="element in thisSeriesArray" :key="element.id" :thisSeries="element"/>
        </div>
      </div>
      <div v-else class="tv-series not-found">
        <h2>TV Series not Found</h2>
      </div>
    </div>
  </section>
</template>

<script>
// *IMPORTS
import FilmCardComponent from "./FilmCardComponent.vue";
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
      
    }
  },
  methods: {
    
  },
  mounted() {
    
  }
}
</script>

<style lang="scss" scoped>
// *COMMON
.flex {
  gap: 0.5rem;
  overflow-x: auto;
}
.tv-series {
  margin-top: 2rem;
}
h2 {
  margin-bottom: 0.3rem;
  color: #fff;
}
</style>