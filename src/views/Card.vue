<template>
  <div class="container">
    <div class="input_zone">
      <input type="text" placeholder="Digite o nome do pokemon..."/>
      <button type="button">Buscar</button>
    </div>
    
    <component-carta
      :lista="pokemons"
    ></component-carta>
  </div>
</template>

<script>
import ComponentCarta from '../components/ComponentCarta.vue'

export default {
  name: 'home',
  
  components: {
    ComponentCarta
  },

  data () {
    return {
      pokemons: []
    }
  },

  mounted () {
    this.listaPokemonGet()
  },

  methods: {
    axioGet (url) {
      return this.$axios.get(url)
        .then((response) => {
          return response.data
        })
        .catch((error) => {
          console.log(error)
        })
    },

    listaPokemonGet () {
      let url = 'https://pokeapi.co/api/v2/pokemon?offset=0&limit=9'
      this.itemPokemons(this.axioGet(url))
    },

    itemPokemons (promisse) {
      promisse.then((listaPokemons) => {
        listaPokemons.results.forEach(pokemon => {
          this.pokemonInfo(this.axioGet(pokemon.url))
        }) 
      })
    },

    pokemonInfo (promisse) {
      promisse.then((listaInfo) => {
        this.pokemons.push(listaInfo)
      })
    }

  }

}
</script>

<style>
  .container{
    display: flex;
    flex-direction: column;
    background-color: darkgray;
  }

  .input_zone{
    width: 100%;
    height: 60px;
    align-items: center;
    display: flex;
    flex-direction: row;
    background-color:cadetblue;
    border: 2px solid black;
    margin-bottom: 30px;
  }
  .input_zone input{
    width: 500px;
    height: 30px;
    margin: 10px;
  }

  .input_zone button{
    width: 200px;
    height: 30px;
  }
</style>

