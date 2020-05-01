<template>

  <div id="app">
    <tareas></tareas>
  </div>

</template>

<script>
import Tareas from "./components/Tareas";

export default {
  name: 'App',
  components:{Tareas},
  created() {
    this.$store.commit('agregarTarea','jola')
  }

}
</script>

<style>

</style>
