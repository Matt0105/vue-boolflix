<template>
  <main>
    <div v-if="arrayFilms.film" class="films-container">
        <ul>
            <FilmCard 
                v-for="(film, index) in arrayFilms.film"
                :key=index+film.id
                :title="film.title"
                :originalTitle="film.original_title"
                :language="film.original_language"
                :vote="film.vote_average"
                :poster="film.poster_path"
                :overview="film.overview.length > 0 ? film.overview : 'No Description'"
            />
        </ul>
        
    </div>
    
    <div v-if="arrayFilms.series" class="series-container">
        <ul>
            <FilmCard 
                v-for="(serie, index) in arrayFilms.series"
                :key=index+serie.id
                :title="serie.name"
                :originalTitle="serie.original_name"
                :language="serie.original_language"
                :vote="serie.vote_average"
                :poster="serie.poster_path"
            />
        </ul>
    </div>
    
    
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
        arrayFilms: Object,  //arrayFilms è un oggetto che contiene un array per i film e un array per le serie tv
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