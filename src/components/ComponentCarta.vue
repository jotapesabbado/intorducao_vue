<template>
    <div class="colecao">    
        <div class="carta" 
            v-for="pokemon in lista"
        >
            <span class="title">{{pokemon.species.name}}</span>
            <img class="img" :src="pokemon.sprites.front_default"/>
            <div class="atribute_zone">
                <p>{{pokemon.moves[0].move.name}}</p>
                <p>{{pokemon.moves[1].move.name}}</p>
                <p>{{pokemon.moves[2].move.name}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ComponentCarta',

    props: {
        lista: []
    }
}
</script>

<style>
  .colecao{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .carta{
    color: black;
    width: 250px;
    border: 2px solid black;
    background-color: grey;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 10px;
  }
  .title{
    font-size: 30px;
    text-transform: capitalize;
  }
  .carta img{
    display: flex;
    border: 2px solid black;
    height: 180px;
    width: 80%;
  }
  .atribute_zone{
    margin-top: 5px;
    width: 98%;
    display: flex;
    background-color: white;
    flex-direction: column;
  }

  .atribute_zone p{
    border-bottom: 2px solid black;
  }
</style>
