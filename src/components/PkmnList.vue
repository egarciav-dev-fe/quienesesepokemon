<script>
import axios from 'axios'

export default {
  name: 'PkmnList',
  data() {
    return {
      pokemonList: []
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
      return ''
    }
  }
}
</script>
