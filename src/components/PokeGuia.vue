<template>
<div>
    <div class="searchBar">
        <a href=""><img class="cardLogo" src="../assets/svg/pokemon_logo.svg" alt=""></a>
        <input class="cardInput" v-model="searchInput" type="text" placeholder="¿Qué pokémon deseas buscar?">
        <button class="cardBtn" @click="search"><img src="../assets/svg/search_white_24dp.svg" alt="Botón de buscar"></button>
    </div>
    <ul id="foundResult" class="searchResult">
    <li><img alt="Foto de Pokemon" class="resultImg" v-bind:src="displayData[0].img"></li>
        <li>{{displayData[0].name}}</li>
        <li>Movimientos: {{displayData[0].moves}}</li>
        <li>Habilidades: {{displayData[0].abilityOne.name}}</li>
        <li>{{displayData[0].abilityTwo.name}}</li>
    </ul>
</div>
</template>

<script>
export default {
    data: () => ({
        searchInput: '',
        displayData: [],
        pokemonData: []
    }),
    methods: {
        search() {
            fetch(`https://pokeapi.co/api/v2/pokemon/` + this.searchInput)
        .then(response => response.json())
        .then((json) => (this.pokemonData = json))
        console.log(this.pokemonData, this.pokemonData.moves[0][0].move.name)
        this.displayData.shift()
        this.displayData.push({
            name: this.pokemonData.name,
            img: this.pokemonData.sprites.front_default,
            abilityOne: this.pokemonData.abilities[0].ability,
            abilityTwo: this.pokemonData.abilities[1].ability,
            moves: this.pokemonData.moves,
        })
        }
    },
    created() {
        this.displayData.shift()
        this.displayData.push({
            name: "pikachu",
            img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png",
            abilityOne: "static",
            abilityTwo: "lightning-rod",
            moves: "mega-punch",
        })
    },
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
        grid-template-rows: repeat(3, 1fr);
        grid-column-gap: 3em;
        grid-template-areas: "img name"
                            "img info"
                            "img info";
    }
    .searchResult li {
        list-style-type: none;
    }
    .resultImg {
        grid-area: img;
        border-radius: 13em;
    }
    .resultName {
        grid-area: name;
    }
    .resultInfo {
        grid-area: info;
    }
</style>