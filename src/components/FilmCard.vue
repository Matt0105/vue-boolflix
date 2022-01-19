<template>
  <div class="card-container">
      <ul>
          <li>{{title}}</li>
          <li>{{originalTitle}}</li>
          <li><img :src="getImgUrl()" alt=""></li>
          <li>{{vote}}</li>
          <!-- <li><img :src="basicImageURL + filmInfo.poster_path" alt=""></li> -->
      </ul>
  </div>

</template>

<script>
export default {
    name: "FilmCard",
    data() {
        return {
            basicImageURL: "https://image.tmdb.org/t/p/original",   
        }
    },
    props: {
        title: String,
        originalTitle: String,
        language: String,
        vote: Number
    },
    methods: {
        getImgUrl() {
            switch (this.language) {
                case "it":
                    return require("../assets/img/italy.png");

                case "en":
                    return require("../assets/img/english.png");

                case "fr":
                    return require("../assets/img/france.png");

                case "ja":
                    return require("../assets/img/japanese.png");

                case "nl":
                    return require("../assets/img/netherlands.png");

                case "pt":
                    return require("../assets/img/portugal.png");
                    
                case "es":
                    return require("../assets/img/spain.jpeg");

                case "de":
                    return require("../assets/img/de.png");

                case "cs":
                    return require("../assets/img/cs.png");

                case "po":
                    return require("../assets/img/po.png");
                    
                case "no":
                    return require("../assets/img/no.png");

                case "sr":
                    return require("../assets/img/sr.png");

                case "tr":
                    return require("../assets/img/turkey.png");

                default:
                    return require("../assets/img/No_flag.svg");
            }

            
        }
    }
}
</script>

<style lang="scss" scoped>

</style>