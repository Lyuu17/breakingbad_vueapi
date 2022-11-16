<template>
  <div>
    <UIBuscar @buscarDatos="buscarDatos" @toggleListaFav="toggleListaFav" :buscando="buscando" :mostrar_fav="mostrar_fav"/>
    <UIDatos :datos="lista" @verInfoPersonaje="verInfoPersonaje"/>
    <UIPersonajeInfo :personaje_info="personaje_info" :en_favoritos="lista_enfavoritos" @toggleFav="toggleFav" @cerrarPersonajeInfo="cerrarPersonajeInfo"/>
  </div>
</template>

<script>
import axios from 'axios';

import Buscar from "./components/Buscar.vue";
import Datos from "./components/Datos.vue";
import PersonajeInfo from './components/PersonajeInfo.vue';

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
  obtenerPersonajePorId(id) {
    return this.obtenerPersonajes(`/${id}`);
  }
  obtenerPersonajes(args = "") {
    return axios.get(`${this.baseurl}/characters${args}`);
  }
};

export default {
  name: "BreakingBadAPI",
  data() {
    return {
      api: new BreakingBadAPI(),
      lista_datos: [],
      lista_favoritos: [],
      mostrar_fav: false,
      buscando: false,
      personaje_info: null
    }
  },
  components: {
    Buscar,
    Datos,
    PersonajeInfo
  },
  emits: ["buscarDatos", "verInfoPersonaje", "toggleFav", "toggleListaFav", "cerrarPersonajeInfo"],
  methods: {
    async buscarDatos(texto) {
      this.buscando = true;
      this.mostrar_fav = false;

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
    verInfoPersonaje(id) {
      this.personaje_info = this.lista[id];
    },
    toggleFav() {
      this.lista_enfavoritos ? this.lista_favoritos = this.lista_favoritos.filter((e) => e.char_id != this.personaje_info.char_id) : this.lista_favoritos.push(this.personaje_info);

      localStorage.setItem("lista_favoritos", JSON.stringify(this.lista_favoritos));
    },
    toggleListaFav() {
      this.mostrar_fav = !this.mostrar_fav;
    },
    cerrarPersonajeInfo() {
      this.personaje_info = null;
    }
  },
  async created() {
    let item = localStorage.getItem("lista_favoritos");
    if (item)
      this.lista_favoritos = JSON.parse(item);
  },
  computed: {
    lista_enfavoritos() {
      return this.personaje_info == null ? false : this.lista_favoritos.filter((e) => e.char_id == this.personaje_info.char_id).length > 0;
    },
    lista() {
      return !this.mostrar_fav ? this.lista_datos : this.lista_favoritos;
    }
  }
}
</script>

<style scoped>

</style>