<template>
  <div id="app">
    <Header 
      @sendToApp="getSearch($event)"
    />
    <Main 
      :input="inputSearch"
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
      inputSearch: "",
    }
  },

  methods: {
    getSearch(value) {
      this.inputSearch = value;
    },

  }
};
</script>

<style lang="scss">
#app {
  
}
</style>
