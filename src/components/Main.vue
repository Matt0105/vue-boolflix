<template>
  <main>
      <ul v-for="(film, index) in arrayFilms" :key=index>
          <li>{{film.title}}</li>
          <li>{{film.original_title}}</li>
          <li>{{film.original_language}}</li>
          <li>{{film.vote_average}}</li>
      </ul>

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
export default {
    name: "Main",
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