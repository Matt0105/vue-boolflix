<template>
  <div class="search-container">
      <input type="text" v-model="searchText">
      <button @click="sendInput()">Cerca</button>
  </div>
</template>

<script>
export default {
    name: "Search",

    data() {
        return {
            searchText: "",
        }
    },

    methods: {
        sendInput() {
            this.$emit("sendSearch", this.searchText);
        }
    }

}
</script>

<style>

</style>