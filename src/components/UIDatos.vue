<template>
  <div class="flex justify-center ml-5 mr-5 p-5 border border-solid bg-green-700">
    <table class="table-fixed w-full border-collapse border border-solid bg-white">
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
        <UIDatosEntrada v-for="(e, i) in datos" :key="i" :datos="e" :id="i" @verInfoPersonaje="verInfoPersonaje"/>
      </tbody>
    </table>
  </div>
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