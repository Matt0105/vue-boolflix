<template>
  <header>
      <div class="header-container">
        <h1>Boolflix</h1>
        <Search 
            @sendSearch="setSearch($event)"
        />
      </div>
      
  </header>
</template>

<script>
import Search from './Search.vue';

export default {
    name: "Header",
    components: {
        Search,
    },

    data() {
        return {
            filmList: {
                film: [],
                series: [],
                firstSearch: true
            },
        }
    },

    methods: {
        setSearch(value) {
            this.filmList = value;
            this.sendSearch();
        },

        sendSearch() {
            this.$emit("sendToApp", this.filmList);
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