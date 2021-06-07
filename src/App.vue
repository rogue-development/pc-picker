<template>
  <v-app>
    <v-app-bar app color="transparent" elevation="0" elevate-on-scroll>
      <span class="text-h5" @click="$router.push('/')" style="cursor: pointer">
        PC Parts API
      </span>
      <v-spacer></v-spacer>

      <v-btn outlined rounded class="accent--text" color="accent" to="login">
        <v-icon class="mr-2" color="accent">mdi-account</v-icon>
        <span class="mr-5">Login</span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>

<style>
.bg-accent {
  background-color: var(--v-accent-base);
}
</style>
