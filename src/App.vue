<template>
  <v-app>
    <v-app-bar app color="deep-purple accent-4" dense dark>
      <!-- -->
      <v-toolbar-title>
        <router-link style="color: white" to="/">Home Page</router-link>
      </v-toolbar-title>
    </v-app-bar>

    <v-content>
      <router-view></router-view>
    </v-content>

    <v-footer app color="deep-purple accent-4" dense dark>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  })
};
</script>
