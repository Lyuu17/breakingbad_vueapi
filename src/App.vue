<template>
  <div>
    <UIBuscar @buscarDatos="buscarDatos" :buscando="buscando"/>
    <UIDatos :datos="lista_datos" @verInfoPersonaje="verInfoPersonaje"/>
  </div>
</template>

<script>
import axios from 'axios';

import UIBuscar from "./components/UIBuscar.vue";
import UIDatos from "./components/UIDatos.vue";

class BreakingBadAPI {
  constructor() {
    this.baseurl = "https://www.breakingbadapi.com/api";
  }
  obtenerPersonajesPorNombre(texto, limite) {
    return this.obtenerPersonajesLimite(`&name=${texto}`, limite);
  }
  obtenerPersonajesPorCategoria(texto, limite) {
    return this.obtenerPersonajesLimite(`&category=${texto}`, limite);
  }
  obtenerPersonajesLimite(args, limite) {
    return this.obtenerPersonajes(`?limit=${limite}${args}`);
  }
  obtenerPersonajes(args) {
    let url = `${this.baseurl}/characters${args}`;
    return axios.get(url);
  }
};

export default {
  name: "BreakingBadAPI",
  data() {
    return {
      api: new BreakingBadAPI(),
      lista_datos: [],
      buscando: false
    }
  },
  created: () => {
  },
  components: {
    UIBuscar,
    UIDatos
  },
  emits: ["buscarDatos", "verInfoPersonaje"],
  methods: {
    async buscarDatos(texto) {
      this.buscando = true;

      const result = await this.api.obtenerPersonajesPorNombre(texto, 100);
      if (result.data == null)
        alert("Fallo al obtener personajes");
      else
      {
        if ((this.lista_datos = result.data).length == 0)
          alert("No se encontraron datos");
      }

      this.buscando = false;
    },
    verInfoPersonaje(char_id) {
      alert("ver info " + char_id);
    }
  }
}
</script>

<style scoped>

</style>