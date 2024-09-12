<script>
export default {
  name: 'PkmnCard',
  props: {
    pokemonName: {
      type: String
    },
    imageUrl: {
      type: String
    }
  },
  data() {
    return {
      userInput: '',
      correct: false
    }
  },
  methods: {
    sendName() {
      if (this.userInput.toLowerCase().trim() == this.pokemonName.toLowerCase()) {
        this.correct = true
        this.$emit('send-name', this.pokemonName)
      } else {
        alert('Vuelve a Intentarlo')
      }
    }
  }
}
</script>

<template>
  <div class="card">
    <img :class="!correct ? 'filter' : ''" :src="imageUrl" alt="pokemonName" />
    <div v-if="correct">
      <p class="name">{{ pokemonName }}</p>
    </div>
    <form v-else @submit.prevent="sendName">
      <input v-model="userInput" />
      <button>Descubrir</button>
      <!-- <p class="incorrect" v-show="correct == false">Incorrecto, Prueba otra vez</p> -->
    </form>
  </div>
</template>

<style scoped>
.filter {
  filter: blur(5px) grayscale(100%);
}
img {
  width: 40%;
}
</style>
