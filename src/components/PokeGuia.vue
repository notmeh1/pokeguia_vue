<template>
<div>
    <div class="searchBar">
        <a href=""><img class="cardLogo" src="../assets/svg/pokemon_logo.svg" alt=""></a>
        <input class="cardInput" v-model="searchInput" type="text" placeholder="¿Qué pokémon deseas buscar?">
        <button class="cardBtn" @click="search"><img src="../assets/svg/search_white_24dp.svg" alt="Botón de buscar"></button>
    </div>
    <div id="foundResult" class="searchResult">
        <img class="pokeImg" :src="displayData[0].img" alt="Foto de Pokemon">
        <h2 class="pokeName">{{displayData[0].name}}</h2>
        <ul class="pokeMoves">
            <h4>Movimientos</h4>
            <li>{{displayData[0].moves[0].move.name}}</li>
            <li>{{displayData[0].moves[1].move.name}}</li>
        </ul>
        <ul class="pokeAbilities">
            <h4>Habilidades</h4>
            <li>{{displayData[0].abiltiyOne}}</li>
            <li>{{displayData[0].abiltiyTwo}}</li>
        </ul>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    data: () => ({
        searchInput: '',
        pokemonData: null,
        displayData: [],
    }),
    methods: {
        search() {
            this.displayData.shift()
            axios
            .get(`https://pokeapi.co/api/v2/pokemon/${this.searchInput}`)
            .then((data) => {
                this.pokemonData = data.data
                this.displayData.push({
                    img: this.pokemonData.sprites.front_default,
                    name: this.pokemonData.name,
                    moves: this.pokemonData.moves,
                    abiltiyOne: this.pokemonData.abilities[0].ability.name,
                    abiltiyTwo: this.pokemonData.abilities[1].ability.name,
                })
                console.log(this.pokemonData)
            })
        }
    },
    created() {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/pikachu`)
        .then((data) => {
            this.pokemonData = data.data
            this.displayData.push({
                    img: this.pokemonData.sprites.front_default,
                    name: this.pokemonData.name,
                    moves: this.pokemonData.moves,
                    abiltiyOne: this.pokemonData.abilities[0].ability.name,
                    abiltiyTwo: this.pokemonData.abilities[1].ability.name,
            })
        })
    }
}
</script>

<style scoped>
    .searchBar {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        width: 55%;
        border-radius: 2em;
        margin-top: 3em;
    }
    .searchBar * {
        color: #ffffff;
    }
    .cardLogo {
        padding: 0 1em;

    }
    .cardInput {
        color: #000000;
        width: 85%;
        height: 2.75em;
        border: 0;
        border-radius: 2em 0 0 2em;
    }
    .cardInput[type=text] {
        width: 100%;
        padding: 1.75em 1em;
        margin: 5px 0;
        box-sizing: border-box;
    }
    .cardInput:focus {
        outline: none;
    }
    .cardBtn {
        background-color: #3399ff;
        border: 0;
        border-radius: 0 2em 2em 0;
        cursor: pointer;
        transition: background-color 0.3s;
        padding: 0.74em;
    }
    .cardBtn:hover {
        background-color: #0080ff;
    }
    .cardBtn:active {
        background-color: #0066cc;
    }
    .searchResult {
        background-color: #2d3848;
        color: #ffffff;
        border-radius: 1.5em;
        padding: 2.5em;
        margin-top: 3em;
        box-shadow: 7px 5px 14px 0px rgba(0,0,0,0.84);
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-column-gap: 2em;
        grid-template-rows: 1fr 2em 1fr 1fr;
        grid-template-areas: "img img"
                            "name name"
                            "moves abilities"
                            "moves abilities";
    }
    .pokeImg {
        display: block;
        margin: 0 auto;
        grid-area: img;
        border-radius: 13em;
    }
    .pokeName {
        grid-area: name;
        text-align: center;
        margin: 0;
    }
    .pokeMoves {
        grid-area: moves;
        padding: 0;
    }
    .pokeAbilities {
        grid-area: abilities;
        padding: 0;
    }
</style>