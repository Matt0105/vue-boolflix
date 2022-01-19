<template>
  <div class="card-container">
      <ul>
          <li>{{filmInfo.title}}</li>
          <li>{{filmInfo.original_title}}</li>
          <li>{{filmInfo.original_language}}</li>
          <li>{{filmInfo.vote_average}}</li>
      </ul>
  </div>
</template>

<script>
export default {
    name: "FilmCard",
    props: {
        filmInfo: Object,
    }
}
</script>

<style lang="scss" scoped>

</style>