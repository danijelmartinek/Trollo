<template>
  <v-app id="mainComponent" dark>

    <Header v-on:toggleDrawer="toggleDrawer()"></Header>

    <Sidebar v-bind:drawer="drawer"></Sidebar>

    <v-content>
      <v-layout>
        <Board></Board>
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
