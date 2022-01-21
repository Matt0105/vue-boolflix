<template>
  <main>
    <div class="main-container">
        <div v-if="arrayFilms.film.length > 0" class="films-container">

            <h2 class="section" v-if="arrayFilms.film">Film</h2>

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
                    :id="film.id"
                    :type="`movie`"
                    :filmGenres="film.genre_ids"

                    :genreChoice="choice"


                />
            </ul>
        </div>
        <div v-else-if="!arrayFilms.firstSearch">
            <h2 class="section">Non sono stati trovati film</h2>
        </div>
    
        <div v-if="arrayFilms.series.length > 0" class="series-container">

            <h2 class="section" v-if="arrayFilms.series">Serie TV</h2>

            <ul>
                <FilmCard 
                    v-for="(serie, index) in arrayFilms.series"
                    :key=index+serie.id
                    :title="serie.name"
                    :originalTitle="serie.original_name"
                    :language="serie.original_language"
                    :vote="serie.vote_average"
                    :poster="serie.poster_path"
                    :overview="serie.overview.length > 0 ? serie.overview : 'No Description'"
                    :id="serie.id"
                    :type="`tv`"
                    :filmGenres="serie.genre_ids"

                    :genreChoice="choice"
                />
            </ul>
        </div>
        <div v-else-if="!arrayFilms.firstSearch">
            <h2 class="section">Non sono state trovate serie TV</h2>
        </div>
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
        choice: Number
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

    .main-container {
        width: 90%;
        margin: auto;
        padding: 2rem 0;

        .films-container, .series-container {
            
            ul {
                display: flex;
                flex-wrap: wrap;
                margin: 1rem 0 4rem 0;
                gap: 1.5rem;
            }
        }

        .section {
                font-size: 2rem;
                font-family: 'Bebas Neue', cursive;
                color: white;
                letter-spacing: 2px;
            }
    }
</style>