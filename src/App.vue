<template>
  <v-app>
    <v-app-bar app color="transparent" elevation="0" elevate-on-scroll>
      <v-icon
        color="accent"
        :size="$vuetify.breakpoint.smAndDown ? '30' : '40'"
        class="mr-3"
        >mdi-desktop-mac</v-icon
      >
      <span
        v-if="!$vuetify.breakpoint.smAndDown"
        class="text-body-1"
        @click="$router.push('/')"
        style="cursor: pointer"
      >
        PC Parts API
      </span>

      <v-spacer></v-spacer>

      <v-btn
        text
        :class="{
          'mr-4': !$vuetify.breakpoint.smAndDown,
          'pa-0': $vuetify.breakpoint.smAndDown,
        }"
      >
        <v-icon v-if="!$vuetify.breakpoint.smAndDown">mdi-github</v-icon>
        <span>Website</span>
      </v-btn>
      <v-btn
        text
        :class="{
          'mr-4': !$vuetify.breakpoint.smAndDown,
          'pa-0': $vuetify.breakpoint.smAndDown,
        }"
      >
        <v-icon v-if="!$vuetify.breakpoint.smAndDown">mdi-github</v-icon>
        <span>API</span>
      </v-btn>

      <v-btn
        outlined
        rounded
        class="accent--text"
        color="accent"
        to="login"
        v-if="!isLoggedIn"
      >
        <v-icon
          :class="{
            'mr-2': !$vuetify.breakpoint.smAndDown,
            'pa-0': $vuetify.breakpoint.smAndDown,
          }"
          color="accent"
          >mdi-account</v-icon
        >
        <span v-if="!$vuetify.breakpoint.smAndDown">Login</span>
      </v-btn>
      <v-btn outlined rounded class="accent--text" color="accent" v-else>
        <v-icon
          :class="{
            'mr-2': !$vuetify.breakpoint.smAndDown,
            'pa-0': $vuetify.breakpoint.smAndDown,
          }"
          color="accent"
        >
          mdi-account
        </v-icon>
        <span v-if="!$vuetify.breakpoint.smAndDown">Account</span>
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

  computed: {
    isLoggedIn: function () {
      return this.$store.state.loggedIn;
    },
  },

  data: () => ({
    //
  }),

  created() {
    let authCookie = this.$cookie.get("_PCPARTS.AUTH");

    if (authCookie != null) {
      this.$store.commit("setLoggedIn", true);
    }
  },

  mounted() {
    console.log(process.env.VUE_APP_GRAPHQL_API_URL);
  },
};
</script>

<style>
.bg-accent {
  background-color: var(--v-accent-base);
}

body,
html {
  width: 100%;
  height: 100%;
  margin: 0px;
  padding: 0px;
  overflow-x: hidden !important;
  overflow-y: auto !important;
}
</style>
