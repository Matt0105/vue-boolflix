<template>
  <main>
    <FilmCard 
        v-for="(film, index) in arrayFilms"
        :key=index
        :filmInfo="film"
    />
      <!--  
            backdrop_path: (...)  immagine
            original_title: (...)
            overview: (...)
            poster_path: (...)
            release_date: (...)
            title: (...)
            vote_average: (...) -->
  </main>
</template>

<script>
// 209546ea776ec96053d1a5aabf76772f  myApi KEY
import FilmCard from './FilmCard.vue';

export default {
    name: "Main",
    components: {
        FilmCard,
    },
    props: {
        arrayFilms: Array,
    },

    data() {
        return {
            
        }
    },

    computed: {

    }
    
}
</script>

<style lang="scss" scoped>

</style>