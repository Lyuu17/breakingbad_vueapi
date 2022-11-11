<template>
  <button @click="verInfo" class="text-white right-2.5 bottom-2.5 bg-green-700 hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-green-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800">
    Ver más
  </button>
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true
    }
  },
  methods: {
    verInfo() {
      this.$emit("verInfoPersonaje", this.id);
    }
  }
}
</script>

<style scoped>

</style>