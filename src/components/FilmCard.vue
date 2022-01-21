<template>
  <div v-if="filmGenres.includes(genreChoice)" @mouseover="learnMore()" class="card-container">
        <li>
            <img v-if="poster" class="poster" :src="basicImageURL + poster" alt="">
            <img v-else class="no-poster" src="../assets/img/noPoster.jpeg" alt="">
        </li>
        <div class="info-container">
            <li class="film-info"> <span class="label">Titolo: </span> {{title}} {{genreChoice}}</li>
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

            <transition name="fade">
                <li v-if="!learnMoreClick" class="film-info" key=1>
                    <span class="label">Descrizione:</span>
                    <p class="desc">{{overview}}</p>
                </li>
            </transition>

            <transition name="fade">
                <li v-if="learnMoreClick" class="film-info" key=2> 
                    <span class="label">Cast: </span>
                    <p 
                        v-for="(actor, index) in castName"
                        :key="index"
                        >
                        {{actor}}
                    </p>
                </li>
            </transition>
            <transition name="fade">
            
                <li v-if="learnMoreClick" class="film-info" key=2> 
                    <span class="label">Generi Correlati: </span>
                    <p 
                        v-for="(genre, index) in filmGenresName"
                        :key="index"
                        >
                        {{genre}}
                    </p>
                </li>
            </transition>

        </div>
        <button @click="test() ,learnMoreClick = !learnMoreClick">Scopri di più ></button>
        
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
            genres: [],
            learnMoreClick: false,
            filmGenresName: []
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
        filmGenres: Array,
        genreChoice: Number
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

        test() {
            console.log(this.filmGenresName);
        },

        getNewVote(value) {
            if(value != 0) {
                return Math.ceil(((Math.ceil(value)*5)/10));
            }
            else {
                return 1;
            }
            
        },

        learnMore() {  //si potrebbe fare nel Search all'inizio, quando popolo l'oggetto così è più veloce la visualizzazione

            if(this.castName.length == 0) {

                axios.get(`${this.baseUrl}/genre/${this.type}/list?api_key=${this.apiKey}`)
                    .then(res => {
                        this.genres = res.data.genres;
                        console.log(this.genres);
                        // console.log(this.genres);
                        this.transformIdGenres();

                    })
                    .catch(err => console.log(err));


                //https://api.themoviedb.org/3/movie/550/credits?api_key=209546ea776ec96053d1a5aabf76772f
                axios.get(`${this.baseUrl}${this.type}/${this.id}/credits?api_key=${this.apiKey}`)
                    .then(res => {
                        const castList = res.data.cast;

                        this.castName = [];

                        for(let i = 0; i < 5; i++) {
                            this.castName.push(castList[i].name);
                        }

                        // console.log(this.castName);         //potrebbero non esserci attori (cartoni animati)
                    })
                    .catch(err => console.log(err));


                
            }
        
        },

        transformIdGenres() {
            this.filmGenresName = [];
            for(let y=0; y < this.filmGenres.length; y++) {             //ciclo annidato: controllo con indice y l'id corrente del film se è presente nella lista generi (i)

                for(let i=0; i < this.genres.length; i++) {
                    if(this.genres[i].id == this.filmGenres[y]) {
                        // this.filmGenres[y] = this.genres[i].name;
                        this.filmGenresName.push(this.genres[i].name);

                    }
                }
            }
        },


    }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/partials/_variables.scss";
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

        &:hover button {
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
            transition: all 1s;


            .desc {
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
            overflow: hidden;

            transition: all 1s;

            .fade-enter-active {
                transition: opacity 1s;
            }
            .fade-leave-active {
                transition: opacity 1s;
                display: none;
            }

            .fade-enter,
            .fade-leave-to {
                    opacity: 0;
            }

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
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            border: none;
            padding: 1rem;
            font-family: 'Bebas Neue', cursive;
            color: white;
            background-color: $n-red;
            opacity: 0;
            transition: all 0.5s;
            letter-spacing: 2px;
            z-index: 101;

            &:hover {
                cursor: pointer;
                filter: brightness(200%);
            }
        }
    }
</style>