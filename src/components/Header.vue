<template>
  <header>
      <div class="header-container">
        <h1>Boolflix</h1>
        
        <select name="genre" id="genre" v-model="genreChoiced" @change="transformIntoId() ">
            <option value="default" disabled selected="selected">Select Genre</option>
            <option value="all" selected="selected">All</option>
            <option 
                v-for="(genre, index) in genresName"
                :key="index"
                :value="genre">{{genre}}
            </option>
        </select>
        
        <Search 
            @sendSearch="setSearch($event)"
        />

      </div>
      
  </header>
</template>

<script>
import Search from './Search.vue';
import axios from "axios";

export default {
    name: "Header",
    components: {
        Search,
    },

    created() {
        axios.get(`${this.baseUrl}/genre/movie/list?api_key=${this.apiKey}`)
            .then(res => {
                this.genreList = res.data.genres;

                axios.get(`${this.baseUrl}/genre/tv/list?api_key=${this.apiKey}`)
                    .then(res => {
                        let tvGenres = res.data.genres;

                        this.genreList.push(...tvGenres);

                        for(let i=0; i < this.genreList.length; i++) {
                            for(let y=i+1; y < this.genreList.length; y++) {
                                if(this.genreList[i].id == this.genreList[y].id) {                  //ciclo annidato per eliminare i doppioni
                                    this.genreList.splice(i, 1);
                                }
                            }
                        }

                        this.transformIdGenres(this.genreList);

                    })
                    .catch(err => console.log(err));


            })
            .catch(err => console.log(err));
    },

    data() {
        return {
            filmList: {
                film: [],
                series: [],
                firstSearch: true
            },
            genreList: [],
            genresName: [],
            genreChoiced: "default",
            idGenreChoiced: null,
            baseUrl: "https://api.themoviedb.org/3/", // [movie] or [tv] / [id] / credits ? apiKey   
            apiKey: "209546ea776ec96053d1a5aabf76772f",
        }
    },

    computed: {
        
    },

    methods: {
        setSearch(value) {
            this.filmList = value;
            this.sendSearch();
        },

        sendSearch() {
            this.$emit("sendToApp", this.filmList);
        },

        transformIdGenres(value) {
                for(let i=0; i < value.length; i++) {
                    this.genresName.push(this.genreList[i].name); 
                }
            
        },

        sendChoice() {
            if(this.genreChoiced == "all") {
                this.idGenreChoiced = null;
            }
            this.$emit("sendGenre", this.idGenreChoiced);
        },

        transformIntoId() {
            
            this.genreList.forEach(el => {

                if(el.name == this.genreChoiced) {
                    this.idGenreChoiced = el.id;
                }
            });

            this.sendChoice();
        }

    }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/partials/_variables.scss";
@import "../assets/scss/partials/_commons.scss";
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');

    header {
        position: absolute;
        top: 0;
        left: 0;
        background-color: rgba(0,0,0,0.8);
        position: sticky;
        z-index: 100;

        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: auto;
            width: 90%;
            height: 70px;

            select {
                width: 200px;
                height: 40%;
                background-color: rgba(0,0,0,0);
                border: 1px solid white;
                outline: none;
                color: white;
                padding: 0 1rem;
            }

            h1 {
                color: $n-red;
                font-size: 3.5rem;
                font-family: 'Bebas Neue', cursive;
                letter-spacing: 3px;
            }
        }

        
    }

</style>