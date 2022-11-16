<template>
  <tr class="border-b hover:backdrop-brightness-50">
    <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border text-center">{{ datos.name }}</td>
    <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border text-center">{{ datos.birthday }}</td>
    <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border text-center">{{ datos.status }}</td>
    <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border text-center">{{ datos.portrayed }}</td>
    <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border text-center">
      <BotonVerInfo :id="id" @verInfoPersonaje="verInfoPersonaje"/>
    </td>
  </tr>
</template>

<script>
import BotonVerInfo from './BotonVerInfo.vue';

export default {
  props: {
    datos: {
      type: Object,
      required: true
    },
    id: {
      type: Number,
      required: true
    }
  },
  components: {
    BotonVerInfo
  },
  emits: ["verInfoPersonaje"],
  methods: {
    verInfoPersonaje(char_id) {
      this.$emit("verInfoPersonaje", char_id);
    }
  }
}
</script>

<style scoped>

</style>