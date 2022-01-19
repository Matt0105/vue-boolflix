<template>
  <header>
      <Search 
        @sendSearch="setSearch($event)"
      />
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
            filmList: [],
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

    header {
        width: 100%;
        height: 80px;
        border-bottom: 1px solid black;
    }

</style>