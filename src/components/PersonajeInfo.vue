<template>
  <div v-if="personaje_info != null" tabindex="-1" aria-hidden="true" class="flex backdrop-blur-sm justify-center place-items-center overflow-y-auto overflow-x-hidden fixed w-full md:inset-0 md:h-full">
    <div class="relative p-4 w-full max-w-2xl h-full md:h-auto">
      <!-- content -->
      <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
        <!-- header -->
        <div class="flex justify-between items-start p-4 rounded-t border-b dark:border-gray-600">
          <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
            {{ personaje_info.name }} ({{ personaje_info.nickname }})
          </h3>
          <button @click="cerrarPopup" type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white" data-modal-toggle="defaultModal">
            <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
            <span class="sr-only">Cerrar</span>
          </button>
        </div>
        <!-- body -->
        <div class="flex p-6 space-y-6">
          <div class="w-1/3">
            <img :src="personaje_info.img" class="border"/>
          </div>
          <div class="ml-2">
            <p class="text-base leading-relaxed text-gray-500 dark:text-gray-400">
              Cumpleaños: {{ personaje_info.birthday }}
            </p>
            <p class="text-base leading-relaxed text-gray-500 dark:text-gray-400">
              Estado: {{ personaje_info.status }}
            </p>
            <p class="text-base leading-relaxed text-gray-500 dark:text-gray-400">
              Actor/actriz: {{ personaje_info.portrayed }}
            </p>
            <p class="text-base leading-relaxed text-gray-500 dark:text-gray-400">
              Ocupación(es):
              <ul class="list-disc pl-5">
                <li v-for="e, i in personaje_info.occupation" :key="i">
                  {{ e }}
                </li>
              </ul>
            </p>
            <p class="text-base leading-relaxed text-gray-500 dark:text-gray-400">
              Temporadas:
              <span v-for="e, i in personaje_info.appearance" :key="i">
                {{ e }}<span v-if="i != personaje_info.appearance.length-1">, </span>
              </span>
            </p>
          </div>
        </div>
        <!-- footer -->
        <div class="flex items-center p-6 space-x-2 rounded-b border-t border-gray-200 dark:border-gray-600">
          <button @click="toggleFav" type="button" :class="colorFav" class="text-white focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">
            {{ textoFav }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    personaje_info: {
      required: true
    },
    en_favoritos: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    cerrarPopup() {
      this.$emit("cerrarPersonajeInfo");
    },
    toggleFav() {
      if (this.en_favoritos)
      {
        if (confirm("¿Estás seguro de eliminar de favoritos a este personaje?"))
          this.$emit("toggleFav");
      }
      else
        this.$emit("toggleFav");
    }
  },
  computed: {
    textoFav() {
      return this.en_favoritos ? "Eliminar de favoritos" : "Añadir a favoritos";
    },
    colorFav() {
      return this.en_favoritos ?
        "bg-red-700 hover:bg-red-800 dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800"
        : "bg-green-700 hover:bg-green-800 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800";
    }
  }
}
</script>

<style scoped>

</style>