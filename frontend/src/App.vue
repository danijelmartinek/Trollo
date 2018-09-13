<template>
  <v-app
    id="inspire"
    dark
  >
    <Header v-on:toggleDrawer="toggleDrawer()"/>

    <Sidebar v-bind:drawer="drawer"/>

    <v-content>
      <v-layout>
        <Board />
      </v-layout>
    </v-content>
  </v-app>
</template>

<script>
import Header from './components/layout/Header.vue'
import Sidebar from './components/layout/Sidebar.vue'
import Board from './components/board/index.vue'

export default {
  data: () => ({
    drawer: true
  }),
  methods: {
    toggleDrawer: function () {
      this.drawer = !this.drawer
    }
  },
  
  name: 'App',
  components: {
    Header,
    Sidebar,
    Board
  }
}
</script>
