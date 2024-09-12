<script>
import axios from 'axios'
import PkmnCard from '@/components/PkmnCard.vue'

export default {
  name: 'PkmnList',
  components: {
    PkmnCard
  },
  data() {
    return {
      pokemonList: [],
      logo: '/img/logopkmn.png'
    }
  },
  async created() {
    try {
      for (let index = 1; index <= 20; index++) {
        const url = `https://pokeapi.co/api/v2/pokemon/${index}`
        const { data } = await axios.get(url)
        this.pokemonList.push(data)
        this.pokemonList.map((pokemon) => ({
          ...pokemon,
          isOK: undefined
        }))
      }
    } catch (error) {
      console.log(error)
    }
  },
  computed: {
    contador() {
      return this.pokemonList.filter((pokemon) => pokemon.isOK).length
    }
  },
  methods: {
    discovered(pokemonName) {
      // console.log(this.pokemonList)
      const foundPokemon = this.pokemonList.find(
        (pokemon) => pokemon.name.toLowerCase() == pokemonName
      )
      foundPokemon.isOK = true
    }
  }
}
</script>

<template>
  <div class="container">
    <img :src="logo" alt="" />
    <h1>¿Quien es ese Pokemon?</h1>
    <p>Pokemones Descubiertos: {{ contador }}</p>
    <div class="pokemon-container">
      <PkmnCard
        v-for="(pokemon, idx) in pokemonList"
        :key="idx"
        :pokemonName="pokemon.name"
        :imageUrl="pokemon.sprites.front_default"
        @send-name="discovered"
      />
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}
img {
  width: 50%;
}
</style>
