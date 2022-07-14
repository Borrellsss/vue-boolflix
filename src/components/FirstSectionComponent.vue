<template>
  <section>
    <div class="container">
      <div v-if="thisMoviesArray.length > 0" class="movies">
        <h2>Movies</h2>
        <div v-hscroll class="flex">
          <CardComponent v-for="element in thisMoviesArray" :key="element.id" :thisElement="element"/>
        </div>
      </div>
      <div v-else class="movies not-found">
        <h2>Movie not Found</h2>
      </div>
      <div v-if="thisSeriesArray.length > 0" class="tv-series">
        <h2>TV Series</h2>
        <div v-hscroll class="flex">
          <CardComponent v-for="element in thisSeriesArray" :key="element.id" :thisElement="element"/>
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
import CardComponent from "./CardComponent.vue";

export default {
  name: "MainFirstSectionComponent",
  components: {
    CardComponent,
  },
  props: {
    thisMoviesArray: Array,
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
.movies {
  margin-bottom: 2rem;

  &.not-found {
    margin-bottom: 0;
  }
}
h2 {
  margin-bottom: 0.3rem;
  color: #fff;
}
</style>