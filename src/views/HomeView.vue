<template>
  <div class="w-full flex justify-center">
    <input type="text" placeholder="Who's that pokemon?"
    class="mt-10 p-2" />
  </div>

  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div class="m-4 p-2 block bg-green-200 rounded-xl text-2x text-center text-blue-400"
      v-for="(pokemon, index) in pokemons"
      :key="index"
    >
      <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
      {{ pokemon.name }}
    </div>
  </div>

</template>

<script>
// @ is an alias to /src
import {onMounted, reactive, toRefs} from 'vue';

export default {
  name: 'HomeView',
  setup() {
    const state = reactive({
      pokemons: []
    }) 

    Promise.all([...Array(1126).keys()].map(id =>
      fetch(`https://pokeapi.co/api/v2/pokemon/${id+1}`).then(resp => resp.json())
      .then(data => {
        state.pokemons.push(data)
      })
    ))
      
      return {...toRefs(state)}
  }, 
  
}

</script>
