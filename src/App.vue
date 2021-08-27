<template>
  <div class="container text-center">
    <img width="400" class="text-center" src="./assets/pokemon-logo.jpg" />
    <h1>PokeGuía</h1>
    <input
      class="form-control"
      placeholder="Escribe el nombre de tu pokemon"
      type="text"
      v-model="escribirPokemon"
      v-on:keyup.enter="buscarPokemon"
    />
    <button class="btn btn-success mt-3" @click="buscarPokemon">
      Buscar pokemon</button
    ><br />

    <img :src="imagenPokemon" alt="" />
    <div>
      <h3>Habilidades</h3>

      <div v-for="(habilidad, index) in habilidades" :key="index">
        {{ habilidad.ability.name }}
      </div>
    </div>
    <div>
      <h3 class="mt-4">Movimientos</h3>

      <div v-for="(movimiento, index) in movimientos" :key="index">
        {{ movimiento.move.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    pokemon: {
      habilidades: [],
      movimientos: [],
    },
    escribirPokemon: "pikachu",
  }),

  created() {
    this.buscarPokemon();
  },

  methods: {
    async buscarPokemon() {
      try {
        const data = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${this.escribirPokemon}`
        );
        const objeto = await data.json();
        this.pokemon = objeto;
      } catch (e) {
        console.log(e);
      }
    },
  },

  computed: {
    imagenPokemon() {
      return this.pokemon?.sprites?.front_default ?? "";
    },
    habilidades() {
      return this.pokemon.abilities;
    },
    movimientos() {
      return this.pokemon.moves;
    },
  },
};
</script>

<style></style>