<template>
  <div class="card-container">
        <li><img :src="basicImageURL + poster" alt=""></li>
        <div class="info-container">
            <li class="film-info"> <span class="label">Titolo: </span> {{title}}</li>
            <li class="film-info"><span class="label">Titolo originale: </span> {{originalTitle}}</li>
            <li class="film-info"><span class="label">Lingua originale: </span> <img class="flag" :src="getImgUrl()" alt=""></li>
            <li class="film-info">
                <span class="label">Voto: </span>
                <i 
                v-for="(star, index) in getNewVote(vote)"
                :key=index
                class="fa-solid fa-star rate"></i>
                <!-- stella da inserire con npm  -->
            </li>
            <li class="film-info"> <span class="label">Descrizione: </span> {{overview}}</li>

        </div>
        
  </div>

</template>

<script>



export default {
    name: "FilmCard",
    data() {
        return {
            basicImageURL: "https://image.tmdb.org/t/p/w342",   
        }
    },
    props: {
        title: String,
        originalTitle: String,
        language: String,
        vote: Number,
        poster: String,
        overview: String
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
        },

        getNewVote(value) {
            if(value != 0) {
                return Math.ceil(((Math.ceil(value)*5)/10));
            }
            
        }
    }
}
</script>

<style lang="scss" scoped>

    .card-container {
        width: 342px;  //larghezza dell'immagine richiesta all'API
        position: relative;

        li {
            margin: 0.4rem 0;
        }

        .info-container {
            position: absolute;
            top: 1rem;
            left: 0.7rem;
            color: white;
            display: none;

            .label {
                text-transform: uppercase;
                font-size: 1rem;
                font-weight: bold;
            }
            .rate {
                color: rgb(243, 221, 26);
            }
        }
    }
</style>