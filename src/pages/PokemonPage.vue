<template>
  <h1 v-if="!pokemon"> Espere por favor </h1>
  <div v-else>
    <div class="container-img">
      <img class="pokemon-img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pok%C3%A9mon_logo.svg/1200px-International_Pok%C3%A9mon_logo.svg.png" alt="pokemon">
      <div class="container-game-img">
        <img class="game-img" src="https://upload.wikimedia.org/wikipedia/commons/3/37/Game_%28rapper%29_Logo.png" alt="game">
      </div>
    </div>
    <div>
      <p>Pokemons Correctos: {{ rightContador }}</p>
      <p>Pokemons Incorrectos: {{ incorrectContador }}</p>
    </div>
    <h1>¿Quien es este Pokemon?</h1>

    <PokemonPicture
      :pokemonId="pokemon.id"
      :showPokemon="showPokemon" />
    <PokemonsOptions
      :pokemons="pokemonArr" 
      @selection="checkAnswer" />

      <div v-if="showAnswer" class="fade-in container-message">
        <h2> {{ message }}</h2>
        <button class="btn" @click="newNage"> Continuar </button>
      </div> 
      
  </div>
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonsOptions from '@/components/PokemonsOptions.vue'

import getPokemonOptions from '@/helpers/getPokemonOptions'


export default {
  components: { 
    PokemonPicture, 
    PokemonsOptions 
  },
  data(){
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: '',
      rightContador: 0,
      incorrectContador: 0,
    }
  },
  methods: {
    async mixPokemonsArray(){
        this.pokemonArr = await getPokemonOptions()

        const rndInt = Math.floor( Math.random() * 4 )
        this.pokemon = this.pokemonArr[ rndInt ]
      },
      checkAnswer( pokemonID){
        this.showPokemon = true
        this.showAnswer = true
        
        if(pokemonID === this.pokemon.id){
          this.message = `Correcto este pokemon es ${this.pokemon.name}`
          this.rightContador ++
        } else {
          this.message = `Ooops, era ${this.pokemon.name}`
          this.incorrectContador ++ 
        }
        
      },
      newNage(){
        this.pokemon = null
        this.pokemonArr = []
        this.showPokemon = false
        this.showAnswer = false
        this.mixPokemonsArray()
      }
  },
  mounted(){
      this.mixPokemonsArray()
  }
}
</script>

<style scoped>

.pokemon-img{
  width: 300px;
}

.container-game-img{
  position: relative;
  right: 0;
  margin-top: -30px;
  margin-left: 205px;
}

.game-img{
  width: 120px;
} 

.container-message{
  display: flex;
  flex-direction: column;
  align-items: center;
}

.btn{
font-size: 14px;
color: #fff;
background-color: #ffdf51;
padding: 10px 30px;
border: 2px solid #0066cc;
box-shadow: rgb(0, 0, 0) 0px 0px 0px 0px;
border-radius: 50px;
transition : 1000ms;
cursor: pointer;
width: 10rem;
}

.btn:hover{

transition : 1000ms;
padding: 10px 30px;
background-color: #fff;
color: #0066cc;
border: solid 2px #0066cc;
}

</style>