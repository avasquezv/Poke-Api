<template>
  <main>
    <section class="banner">
      <img src="pokemon-banner.jpeg" />
    </section>

    <section class="search">
      <h4>PokeGuía</h4>
      <form class="input-search" @submit.prevent="datosPokemon">
        <p>Nombre:</p>
        <input type="text" v-model="nombrePokemon" required/>
        <button type="submit">Buscar</button>
      </form>
    </section>

    <section>
      <img :src="pokemonFrontDefault" alt="" />
    </section> 

    <section class="movements">
      <h4>Movimientos</h4>
      <ul>
        <li v-for="(move, $index) of pokemonMoves" :key="$index">
          {{ move }}
        </li>
      </ul>
    </section>

    <section class="habilities">
      <h4>Habilidades</h4>
      <ul>
        <li v-for="(abil, $index) of pokemonHabi" :key="$index">
          {{ abil }}

        </li>
      </ul>
    </section>
  </main>
</template>


<script>

export default {
  name: "App",
  data: () => ({
      nombrePokemon:"",
      pokemon: null,
    }),
  computed: {
    pokemonMoves() {
      return (
        this.pokemon &&
        this.pokemon.moves &&
        this.pokemon.moves.map((move) => move.move.name)
      ) || []
    },
    pokemonHabi() {
      return (
        this.pokemon &&
        this.pokemon.abilities &&
        this.pokemon.abilities.map((abil) => abil.ability.name)
      ) || []
    },
    pokemonFrontDefault() {
      return this.pokemon?.sprites?.front_default ?? ""
    }},

  methods: {
    datosPokemon(){
      fetch(`http://pokeapi.co/api/v2/pokemon/${this.nombrePokemon}`)
      .then((response) => response.json())
      .then((pokemon) => (this.pokemon = pokemon))
      }},

  mounted() {},

}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: black;
  color: white;
}

main {
  max-width: 400px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-left: auto;
  margin-right: auto;
}

.banner {
  display: flex;
  align-items: center;
  justify-content: center;
}
.banner img {
  width: 50%;
}

.search {
  text-align: center;
}

.search .input-search {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
}

.search .input-search p {
  margin: 0;
}
</style>
