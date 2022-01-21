<template>
  <div class="card-container">
        <li>
            <img v-if="poster" class="poster" :src="basicImageURL + poster" alt="">
            <img v-else class="no-poster" src="../assets/img/noPoster.jpeg" alt="">
        </li>
        <!-- <li><img class="poster" :src="basicImageURL + poster" alt=""></li> -->
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
            <li class="film-info"> <span class="label">Descrizione: </span> <p>{{overview}}</p></li>

            <button @click="learnMore()">Scopri ></button>

        </div>
        
  </div>

</template>

<script>

import axios from "axios";

export default {
    name: "FilmCard",
    data() {
        return {
            basicImageURL: "https://image.tmdb.org/t/p/w342",
            baseUrl: "https://api.themoviedb.org/3/", // [movie] or [tv] / [id] / credits ? apiKey   
            apiKey: "209546ea776ec96053d1a5aabf76772f",
            castName: [],
            genres: []
        }
    },
    props: {
        title: String,
        originalTitle: String,
        language: String,
        vote: Number,
        poster: String,
        overview: String,
        id: Number,
        type: String,
        filmGenres: Array
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
            else {
                return 1;
            }
            
        },

        learnMore() {
            //https://api.themoviedb.org/3/movie/550/credits?api_key=209546ea776ec96053d1a5aabf76772f
            axios.get(`${this.baseUrl}${this.type}/${this.id}/credits?api_key=${this.apiKey}`)
                .then(res => {
                    const castList = res.data.cast;

                    for(let i = 0; i < 5; i++) {
                        this.castName.push(castList[i].name);
                    }

                    // console.log(this.castName);         //potrebbero non esserci attori (cartoni animati)
                })
                .catch(err => console.log(err));


            axios.get(`${this.baseUrl}/genre/${this.type}/list?api_key=${this.apiKey}`)
                .then(res => {
                    this.genres = res.data.genres;

                    for(let y=0; y < this.filmGenres.length; y++) {             //ciclo annidato: controllo con indice y l'id corrente del film se è presente nella lista generi (i)

                        for(let i=0; i < this.genres.length; i++) {
                            if(this.genres[i].id == this.filmGenres[y]) {
                                this.filmGenres[y] = this.genres[i].name;
                            }
                        }
                    }

                })
                .catch(err => console.log(err));

        }

    }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/partials/_mixins.scss";

    .card-container {
        width: calc(100% / 4 - 1.5rem);
        max-height: 60vh;
        position: relative;
        overflow: hidden;
        transition: all 0.2s;

        &:hover {
            outline: 3px solid white;
            outline-offset: 7px;
            cursor: pointer;
        }

        &:hover .poster {
            transform: rotate3d(0, 1, 0, 180deg);
            filter: brightness(30%);
        }
        &:hover .no-poster {
            transform: rotate3d(0, 1, 0, 180deg);
            filter: brightness(30%);
        }

        &:hover .info-container {
            opacity: 1;
        }

        li {
            height: 100%;
        }
        .poster {
            width: 100%;
            height: 100%;
            transition: all 0.5s;
        }
        .no-poster {
            width: 100%;
            height: 100%;
            transition: all 0.5s;
            object-fit: cover;
            object-position: center;
        }

        li.film-info {
            margin: 0.4rem 0;

            p {
                height: 20vh;
                overflow: scroll;
                margin-top: 5px;
            }
            p::-webkit-scrollbar {
                @include hideScroll;
            }
        }

        .info-container {
            position: absolute;
            top: 1rem;
            left: 0.7rem;
            color: white;
            opacity: 0;

            transition: all 1.3s;

            .label {
                text-transform: uppercase;
                font-size: 1rem;
                font-weight: bold;
            }
            .rate {
                color: rgb(243, 221, 26);
            }
        }

        button {
            position: relative;
            background-color: white;
            z-index: 101;
        }
    }
</style>