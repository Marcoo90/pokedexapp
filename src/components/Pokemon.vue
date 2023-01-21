<template>
  <v-container>
    <v-card class="mx-auto" max-width="344" @click="goToAboutPage(datos)">
      <v-img
        :src="datos.sprites.other.home.front_default"
      ></v-img>
      <v-card-title class="d-flex flex-column">{{ datos.name }}</v-card-title>
    </v-card>
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  name: "pokemon",
  props: {
    pokemonItem: Object
  },
  data: () => ({
    datos: {}
  }),
  mounted() {
    axios.get(this.pokemonItem.url).then((res) => {
      this.datos = res.data
    })
  },
  methods: {
    goToAboutPage(poke) {
      //vamos a la ruta pasando un parametro
      this.$router.push({name:'about', params:{pokemon:poke} })
    }
  },
};
</script>