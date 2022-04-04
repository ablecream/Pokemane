<template>
  <div class="about">
    <div v-if="pokemon" class="w-3/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center">
      <h3 class="text-2xl text-green-800 uppercase">{{pokemon.name}}</h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.other.dream_world.front_default" :alt="pokemon.name">
      </div>
      <h3 class="text-green-500">Types</h3> 
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class="text-blue-900 uppercase">{{type.type.name}}</h5>
      </div>
    </div>
  </div>
</template>
<script>
  import {useRoute} from "vue-router";
  import {reactive, toRefs} from "vue";
  export default {
    setup() {
      const route = useRoute();

      const state = reactive({
        pokemon: null
      })

      fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
        .then((res) => res.json())
        .then((data) => state.pokemon = data)


      return {...toRefs(state)}
    }

  }
</script>
