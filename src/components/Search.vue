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
            apiQuery: "https://api.themoviedb.org/3/search/movie?api_key=209546ea776ec96053d1a5aabf76772f&query=",
            searchText: "",
            filmList: [],
        }
    },

    methods: {
        sendInput() {

            axios.get(this.apiQuery+this.searchText)
                .then(res => {
                    this.filmList = res.data.results;
                    // this.filmList.forEach(el => {

                    //     if(el.original_language == "it") {
                    //         el.original_language = "../assets/img/italy.png";
                    //     }
                    // });

                    this.$emit("sendSearch", this.filmList);

                })
                .catch(err => console.log(err))

        }
    }

}
</script>

<style>

</style>