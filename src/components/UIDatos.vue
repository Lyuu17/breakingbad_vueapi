<template>
  <div class="flex justify-center border border-solid bg-green-700 m-auto pt-2 mt-2 pb-2 mb-2 w-1/2">
    <div class="py-2 inline-block min-w-full sm:px-6 lg:px-8">
      <div class="overflow-x-auto">
        <table class="min-w-full bg-white">
          <thead class="border-b">
            <tr>
              <th scope="col" class="border text-sm font-medium text-gray-900 px-6 py-4 text-center">
                Nombre
              </th>
              <th scope="col" class="border text-sm font-medium text-gray-900 px-6 py-4 text-center">
                Cumpleaños
              </th>
              <th scope="col" class="border text-sm font-medium text-gray-900 px-6 py-4 text-center">
                Estado
              </th>
              <th scope="col" class="border text-sm font-medium text-gray-900 px-6 py-4 text-center">
                Actor/actriz
              </th>
              <th scope="col" class="border text-sm font-medium text-gray-900 px-6 py-4 text-center">
                
              </th>
            </tr>
          </thead>
          <tbody>
            <UIDatosEntrada v-for="(e, i) in datos" :key="i" :datos="e" :id="i" @verInfoPersonaje="verInfoPersonaje"/>
          </tbody>
        </table>
      </div>
    </div>
  </div>
  <!--
  <div class="flex justify-center ml-5 mr-5 p-5 border border-solid bg-green-700">
    <table class="table-fixed overflow-x-scroll min-w-full border-collapse border border-solid bg-white">
      <thead>
          <tr>
            <th class="border">Nombre</th>
            <th class="border">Cumpleaños</th>
            <th class="border">Estado</th>
            <th class="border">Actor/actriz</th>
            <th class="border"></th>
          </tr>
      </thead>
      <tbody>
        
      </tbody>
    </table>
  </div>
  -->
</template>

<script>
import UIDatosEntrada from './UIDatosEntrada.vue';

export default {
  props: {
    datos: {
      type: Array,
      required: true
    }
  },
  emits: ["verInfoPersonaje"],
  components: {
    UIDatosEntrada
  },
  methods: {
    verInfoPersonaje(char_id) {
      this.$emit("verInfoPersonaje", char_id);
    }
  }
}
</script>

<style scoped>

</style>