<template>
    <header>
        <div class="container">
            <div class="flex">
                <div class="header-left-side flex">
                    <div class="logo">
                        <a @click.prevent="$emit('axiosCall', title), resetInput()" href="#">
                            <img src="../assets/img/boolflix-logo.png" alt="boolflix logo">
                        </a>
                    </div>
                    <nav>
                        <ul class="flex">
                            <li>
                                <a href="#">Home</a>
                            </li>
                            <li>
                                <a href="#">TV Shows</a>
                            </li>
                            <li>
                                <a href="#">Movies</a>
                            </li>
                            <li>
                                <a href="#">Originals</a>
                            </li>
                            <li>
                                <a href="#">Recently added</a>
                            </li>
                            <li>
                                <a href="#">My list</a>
                            </li>
                        </ul>
                    </nav>
                </div>
                <div class="header-right-side flex">
                    <select @change="$emit('axiosGenresCall', genre)" name="genres" id="genres" v-model="genre">
                        <option value="null" selected>All</option>
                        <option v-for="(element, index) in genresArray" :key="index" :value="element.id">
                            {{element.name}}
                        </option>
                    </select>
                    <div class="search">
                        <input @keyup.enter="$emit('axiosCall', title), resetInput()" type="text" v-model="title" placeholder="Search">
                        <button @click="$emit('axiosCall', title), resetInput()" class="btn red">Search</button>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
// *IMPORTS
import axios from "axios";

export default {
    name: "HeaderComponent",
    data() {
        return {
            apiKey: "?api_key=f1240ec31fc689a8980fbeb47322e5ec",
            langKey: "&language=en-US",
            allGenresAxiosCall: "https://api.themoviedb.org/3/genre/movie/list",
            title: "",
            genre: null,
            genresArray: [],
        }
    },
    methods: {
        resetInput() {
            this.title = "";
            this.genre = null;
        },
        getGenres() {
            this.allGenresAxiosCall += `${this.apiKey}${this.langKey}`;
            // !DEBUG
            // console.log(this.allGenresAxiosCall);

            axios.get(this.allGenresAxiosCall).then((response) => {
                response.data.genres.forEach(element => {
                    this.genresArray.push(element);
                });
                // !DEBUG
                // console.log(this.genresArray);
            });
        },
    },
    mounted() {
        this.getGenres();
    }
}
</script>

<style lang="scss" scoped>
// *IMPORTS
@import "../style/variables.scss";

// *STYLING
header {
    height: $header-height;
    color: #fff;
    background-color: rgba(0, 0, 0, 0);
    transition: all 300ms;

    &:hover {
        background-color: #000;
        box-shadow: 0 0 10px #000;
    }
    .container {

        .flex {
            height: $header-height;
            justify-content: space-between;
            align-items: center;

            nav {
                margin-left: 2rem;

                li {
                    margin-right: 1.5rem;

                    a {
                        font-size: 0.85rem;
                        font-weight: 300;

                        &:hover {
                            text-shadow: 0 0 1px #fff;
                        }
                    }
                }
            }
        }
    }
}
</style>