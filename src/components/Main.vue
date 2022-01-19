<template>
  <main>
      {{input}}
  </main>
</template>

<script>
// 209546ea776ec96053d1a5aabf76772f  myApi KEY
export default {
    name: "Main",
    props: {
        input: String,
    },

    data() {
        return {
            apiQuery: "https://api.themoviedb.org/3/search/movie?api_key=209546ea776ec96053d1a5aabf76772f&query="
        }
    }
}
</script>

<style lang="scss" scoped>

</style>