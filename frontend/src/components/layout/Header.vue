<template>
  <v-toolbar
    color="red"
    dense
    fixed
    clipped-left
    app
  >
    <v-toolbar-side-icon @click.stop="toggleDrawer()"></v-toolbar-side-icon>
    <v-icon class="mx-1">fa dashboard</v-icon>
    <v-toolbar-title class="mr-5 align-center">
      <span class="title">Trollo</span>
    </v-toolbar-title>
  </v-toolbar>
</template>

<script>

export default {
  data: () => ({
    drawer: false
  }),
  methods: {
    toggleDrawer: function () {
      this.$emit("toggleDrawer")
    }
  },

  name: 'Header'
}
</script>
