<template>
  <v-toolbar
    color="red"
    dense
    fixed
    clipped-left
    app
  >
    <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    <v-icon class="mx-1">fa dashboard</v-icon>
    <v-toolbar-title class="mr-5 align-center">
      <span class="title">Trollo</span>
    </v-toolbar-title>
  </v-toolbar>
</template>

<script>
module.exports = {
  data: function () {
    return {
      greeting: 'Hello'
    }
  }
}
</script>

<style scoped>

</style>
