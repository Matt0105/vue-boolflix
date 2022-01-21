<template>
  <div id="app">
    <Header 
      @sendToApp="getSearch($event)"
      @sendGenre="getChoice($event)"
    />
    <Main 
      :arrayFilms="filmList"
      :choice="idGenreChoiced"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main
  },

  data() {
    return {
      filmList: {
        film: [],
        series: [],
        firstSearch: true
      },
      idGenreChoiced: null,
    }
  },

  methods: {
    getSearch(value) {

      this.filmList = value;
      console.log(this.filmList);
    },

    getChoice(value) {
      this.idGenreChoiced = value;
      console.log(this.idGenreChoiced);
    }
  }
};
</script>

<style lang="scss">
@import "./assets/scss/style.scss";

#app {
  
}
</style>
