<template>
    <h1 v-if="!pokemon">Espere un momento porfavor</h1>
<div v-else>
    <h1>quien es este pokemon ? </h1>
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>
    <PokemonOptions :pokemons="pokemonArr" :count="countP" @selection="checkAnswer($event)" />

    <template v-if="showAnswer">
        <h2  class="fade-in">{{message}} <b style="color:red">{{countP}}</b></h2>
        <button class="btn btn-info" @click="newGame()" >Nuevo juego</button>
    </template>

</div>
</template>

<script>

import PokemonOptions from '@/components/PokemonOptions';
import PokemonPicture from '@/components/PokemonPicture';
import getPokemonsOptions from '@/helpers/getPokemonOptions';
import Sweet from 'sweetalert2';
export default {
    components: { PokemonOptions, PokemonPicture },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: '',
            countP:0
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonsOptions()
            const rndInt = Math.floor(Math.random() * 4)
            this.pokemon=this.pokemonArr[rndInt]
        },
        checkAnswer(selectedID) {
            this.showPokemon = true
            this.showAnswer=true
            
            if (selectedID === this.pokemon.id) {
                this.countP += 1;                
                this.message = `Correcto, ${this.pokemon.name}`
                this.setTimeP()
            } else {
                if (this.countP > 0) {
                    this.countP -= 1;
                }
                this.setTimeP()
                this.message=`Opps, era ${this.pokemon.name}`
            }
        },
        newGame() {
            this.showPokemon = false
            this.showAnswer = false
            this.pokemonArr = []
            this.mixPokemonArray()
            this.message = ''
            this.pokemon = null
            this.countP=0
        },
        setTimeP() {
            setTimeout(() => {
                    this.pokemonArr = []
                    this.pokemon=null
                    this.mixPokemonArray()
                    this.showPokemon = false
                    this.showAnswer=false
            }, 4000);            
        }
        
    },
    mounted() {
        this.mixPokemonArray()
    }
}
</script>

