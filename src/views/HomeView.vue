<template>
  <v-container>
    <v-row class="text-center">
    <v-col cols="12">
      <v-img
        :src="require('../assets/pokemon.png')"
        class="my-3"
        contain
        height="200"
      />
    </v-col>

    <v-container fluid>
      <v-data-iterator
        :items="items"
        :items-per-page="20"
        :search="search"
        hide-default-footer
      >
        <template v-slot:header>
          <div class="pb-12">
            <v-text-field
              v-model="search"
              clearable
              flat
              hide-details
              prepend-inner-icon="mdi-magnify"
              label="Busca tu pokemon"
            ></v-text-field>
          </div>
        </template>

        <template v-slot:default="props">
          <v-row>
            <v-col
              v-for="item in props.items"
              :key="item.name"
              cols="12"
              sm="6"
              md="4"
              lg="3"
            >
              <Pokemon :pokemonItem="item" />
            </v-col>
          </v-row>
        </template>
      </v-data-iterator>
    </v-container>
  </v-row>
  <v-row v-if="error !== ''">
      <p>Ocurrió un problema con el servidor</p>
  </v-row>
  </v-container>
  
</template>

<script>
import axios from "axios";
import Pokemon from "../components/Pokemon";
export default {
  name: "Home",
  components: {
    Pokemon,
  },
  data() {
    return {
      search: "",
      items: [],
      error: "",
    };
  },
  created() {
    this.getokemon();
  },
  methods: {
    // getokemon() {
    //   axios.get('https://pokeapi.co/api/v2/pokemon?limit=20')
    //     .then((response) => {
    //       console.log(response)
    //       this.items = response.data.results
    //     }).catch((err) => {
    //     this.error = err.response.data
    //   })
    // }
    async getokemon() {
      try {
        const response = await axios.get("https://pokeapi.co/api/v2/pokemon?limit=20");
        const { results } = response.data;
        this.items = results;
      } catch (error) {
        this.error = error.response.data;
      }
    },
  },
};
</script>