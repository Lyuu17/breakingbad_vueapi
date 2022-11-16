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
</template>

<script>
import DatosEntrada from './DatosEntrada.vue';

export default {
  props: {
    datos: {
      type: Array,
      required: true
    }
  },
  emits: ["verInfoPersonaje"],
  components: {
    DatosEntrada
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