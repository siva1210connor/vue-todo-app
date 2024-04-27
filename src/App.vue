<template>
  <v-app id="inspire">
    <v-navigation-drawer :width="231" v-model="drawer">
      <v-list-item
        title="Vuetify Todo App"
        subtitle="Organize your tasks"
      ></v-list-item>
      <v-divider></v-divider>
      <v-list-item to="/" link title="Todo"></v-list-item>
      <v-list-item to="/about" link title="About"></v-list-item>
    </v-navigation-drawer>

    <v-app-bar
      color="primary"
      image="https://picsum.photos/1920/1080?random"
      density="prominent"
    >
      <template v-slot:image>
        <v-img
          gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <template v-slot:prepend>
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      </template>

      <v-app-bar-title class="pb-12">Todo App</v-app-bar-title>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from "vue";

const drawer = ref(null);
</script>

<script>
export default {
  data: () => ({ drawer: null }),
};
</script>
