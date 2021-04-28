<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
            Ajouter une tâche
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <HelloWorld/>
    
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Todo list app</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <toDo/>
    </v-main> 
  </v-app>
</template>

<script>
  import HelloWorld from './components/HelloWorld'
  import toDo from './components/toDo'

  export default {
    data: () => ({ drawer: null }),
    components: {
      HelloWorld,
      toDo
    }
  }
</script>