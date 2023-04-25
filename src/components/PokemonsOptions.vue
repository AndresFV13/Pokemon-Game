<template>
  <div class="options-container">
    <ul>
      <li class="options-pokemons"
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit( 'selection', pokemon.id )">
        {{pokemon.name}}
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  props:{
    pokemons:{
      type: Array,
      required: true
    }
  },
  methods: {

  }
}
</script>

<style scoped>
ul {
    list-style-type: none;
}
li {
    background-color: white;
    border-radius: 5px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    cursor: pointer;
    margin-bottom: 10px;
    width: 250px;
}

li:hover {
    background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
    display: flex;
    justify-content: center;
}

.options-pokemons{
font-size: 14px;
font-weight: bold;
color: black;
background-color: #ffdf51;
padding: 10px 30px;
box-shadow: rgb(0, 0, 0) 0px 0px 0px 0px;
border-radius: 50px;
transition : 1000ms;
cursor: pointer;
width: 10rem;
}

.options-pokemons:hover{

transition : 1000ms;
padding: 10px 30px;
background-color: black;
color: white;
border: solid 2px #ffdf51;
}

</style>