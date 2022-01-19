<template>
  <div class="search-container">
      <input type="text" v-model="searchText">
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
                series: []
            },
        }
    },

    methods: {
        sendInput() {

            axios.get(this.filmApiQuery+this.searchText)       //prima chiamata: film
                .then(res => {
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
    }

}
</script>

<style>

</style>