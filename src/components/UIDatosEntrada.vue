<template>
  <tr class="hover:backdrop-brightness-50">
    <td class="border text-center">{{ datos.name }}</td>
    <td class="border text-center">{{ datos.birthday }}</td>
    <td class="border text-center">{{ datos.status }}</td>
    <td class="border text-center">{{ datos.portrayed }}</td>
    <td class="border text-center">
      <UIBotonVerInfo :id="id" @verInfoPersonaje="verInfoPersonaje"/>
    </td>
  </tr>
</template>

<script>
import UIBotonVerInfo from './UIBotonVerInfo.vue';

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
    UIBotonVerInfo
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