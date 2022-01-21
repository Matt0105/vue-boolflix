<template>
  <header>
      <div class="header-container">
        <h1>Boolflix</h1>
        <Search 
            @sendSearch="setSearch($event)"
        />

        <select name="genre" id="genre" v-model="genreChoiced" @change="transformIntoId()">
            <option value="all">All</option>
            <option 
                v-for="(genre, index) in genresName"
                :key="index"
                :value="genre">{{genre}}
            </option>
        </select>
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
                        console.log(this.genreList);
                        this.transformIdGenres(this.genreList);

                        console.log(this.genresList);

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
            genreChoiced: "",
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

            h1 {
                color: $n-red;
                font-size: 3.5rem;
                font-family: 'Bebas Neue', cursive;
                letter-spacing: 3px;
            }
        }

        
    }

</style>