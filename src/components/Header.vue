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
            inputSearch: "",
        }
    },

    methods: {
        setSearch(value) {
            this.inputSearch = value;

            console.log(value);
            console.log(this.inputSearch);

            this.sendSearch();
        },

        sendSearch() {
            this.$emit("sendToApp", this.inputSearch);
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