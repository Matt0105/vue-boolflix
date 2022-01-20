<template>
  <div class="search-container">
      <input @keyup.enter="sendInput()" type="text" v-model="searchText">
      <button @click="sendInput()">Cerca</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Search",

    data() {
        return {
            filmApiQuery: "https://api.themoviedb.org/3/search/movie?api_key=209546ea776ec96053d1a5aabf76772f&query=",
            seriesApiQuery: "https://api.themoviedb.org/3/search/tv?api_key=209546ea776ec96053d1a5aabf76772f&query=",
            searchText: "",
            filmList: {
                film: [],
                series: [],
                firstSearch: true
            },
        }
    },

    methods: {
        sendInput() {

            if(this.searchText.trim() != "") {
                axios.get(this.filmApiQuery+this.searchText)       //prima chiamata: film
                .then(res => {
                    
                    this.filmList.firstSearch = false;

                    this.filmList.film = res.data.results;

                    axios.get(this.seriesApiQuery+this.searchText)  //seconda chiamata: serie TV
                        .then(res => {
                            this.filmList.series = res.data.results;

                            this.$emit("sendSearch", this.filmList);

                        })
                        .catch(err => console.log(err))
                })
                .catch(err => console.log(err))
            }
            else {
                this.filmList = {
                    film: [],
                    series: [],
                    firstSearch: true
                };

                this.$emit("sendSearch", this.filmList);
            }

        }
    }

}
</script>

<style lang="scss" scoped>
@import "../assets/scss/partials/_variables.scss";

    .search-container {
        display: flex;
        align-items: center;
        height: 100%;


        input {
            width: 300px;
            height: 40%;
            background-color: rgba(0,0,0,0);
            border: 1px solid white;
            outline: none;
            color: white;
            padding: 0 1rem;
        }

        button {
            height: 40%;
            border: none;
            background-color: $n-red;
            text-transform: uppercase;
            color: white;
            font-size: 0.8rem;
            cursor: pointer;
            padding: 5px;
            margin-left: 5px;
        }
    }

</style>