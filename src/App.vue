<template>
  <div id="app">
    <Header 
      @sendToApp="getSearch($event)"
    />
    <Main 
      :arrayFilms="filmList"
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
        series: []
      },
    }
  },

  methods: {
    getSearch(value) {

      this.filmList = value;
      console.log(this.filmList);
    },

  }
};
</script>

<style lang="scss">
@import "./assets/scss/style.scss";

#app {
  
}
</style>
