<script>
import Pokemon from './components/Pokemon.vue'

function data() {
  return {
    pokeApiBaseUrl: 'https://pokeapi.co/api/v2/pokemon',
    allPokemon: []
  }
}
async function fetchPokemonList() {
  const res = await fetch(`${this.pokeApiBaseUrl}?limit=151`)
  const finalRes = await res.json()
  finalRes.results.map(async (result) => {
    const pokemon = await fetch(result.url)
    const allPokemonData = await pokemon.json()
    const { id, name, sprites, stats } = allPokemonData
    this.allPokemon.push(
      await { id, name, avatar: sprites.other['official-artwork'].front_default, stats }
    )
  })
}

function sortPokemonList() {
  return this.allPokemon.sort((a, b) => a.id - b.id)
}

export default {
  components: {
    Pokemon
  },
  data,
  methods: {
    fetchPokemonList
  },
  computed: {
    sortPokemonList
  },
  mounted() {
    this.fetchPokemonList()
  }
}
</script>

<template>
  <div class="container">
    <div class="title">List of Kanto Pokemon ({{ allPokemon.length }})</div>
    <Pokemon v-for="pokemon in sortPokemonList" :key="pokemon.id" :pokemon="pokemon" />
  </div>
</template>

<style scoped lang="scss">
body {
  margin: 0;
  padding: 0;
}
.container {
  height: 100%;
  background-color: aliceblue;
  padding: 24px 48px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.title {
  padding: 16px;
  background-color: #212121;
  color: #fff;
  font-size: 48px;
  text-align: center;
  flex-basis: 100%;
  margin-bottom: 64px;
}
</style>
