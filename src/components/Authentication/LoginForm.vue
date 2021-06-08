<template>
  <v-container fluid>
    <p class="d-flex justify-center text-h5 text-sm-h4 text-md-h3 my-16">
      Login
    </p>

    <div class="mb-8 d-flex justify-center">
      <a href="https://google.com" target="_blank" class="text-decoration-none">
        <v-icon
          size="35"
          :class="{
            'mx-10': $vuetify.breakpoint.mdAndUp,
            'mx-5': $vuetify.breakpoint.smAndDown,
          }"
          title="Not implemented yet..."
        >
          mdi-google
        </v-icon>
      </a>
      <a href="https://github.com" target="_blank" class="text-decoration-none">
        <v-icon
          size="35"
          :class="{
            'mx-10': $vuetify.breakpoint.mdAndUp,
            'mx-5': $vuetify.breakpoint.smAndDown,
          }"
          title="Not implemented yet..."
        >
          mdi-github
        </v-icon>
      </a>
      <a
        href="https://discord.com"
        target="_blank"
        class="text-decoration-none"
      >
        <v-icon
          size="35"
          :class="{
            'mx-10': $vuetify.breakpoint.mdAndUp,
            'mx-5': $vuetify.breakpoint.smAndDown,
          }"
          title="Not implemented yet..."
        >
          mdi-discord
        </v-icon>
      </a>
    </div>

    <v-divider class="mb-6" />

    <v-form ref="login" v-model="valid" class="mt-4">
      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="Email"
        prepend-icon="mdi-account"
      />
      <v-text-field
        v-model="password"
        :rules="passwordRules"
        label="Password"
        prepend-icon="mdi-lock"
        :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
        @click:append="showPassword = !showPassword"
        :type="showPassword ? 'text' : 'password'"
      />

      <p>Your session will be saved for 30 days.</p>

      <v-divider />

      <div class="d-flex justify-end mr-2 mt-4">
        <v-btn @click="$refs.login.reset()" text class="mr-2"> Cancel </v-btn>
        <v-btn
          color="accent"
          @click="login"
          :loading="loading"
          :disabled="loading"
        >
          Login
        </v-btn>
      </div>
    </v-form>

    <v-snackbar
      :timeout="4000"
      v-model="snackbar"
      absolute
      bottom
      :color="statusColor"
      outlined
    >
      {{ status }}

      <template v-slot:action="{ attrs }">
        <v-btn color="error" text v-bind="attrs" @click="snackbar = false" icon>
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </template>
    </v-snackbar>
  </v-container>
</template>

<script>
import gql from "graphql-tag";

const env = {
  AUTH_COOKIE_NAME: "_PCPARTS.AUTH",
  COOKIE_DOMAIN: process.env.VUE_APP_COOKIE_DOMAIN,
};

export default {
  name: "Login-form",

  data: () => ({
    valid: true,
    email: "",
    password: "",
    showPassword: false,
    loading: false,

    snackbar: false,
    status: "",
    statusColor: "",

    emailRules: [
      (value) => !!value || "Email is required.",
      (value) =>
        (!!value && value.match(/[^@ \t\r\n]+@[^@ \t\r\n]+\.[^@ \t\r\n]+/)) ||
        "Not a valid email.",
    ],
    passwordRules: [
      (value) => !!value || "Password is required.",
      (value) =>
        (value && value.length > 8) || "Password must be atleast 8 characters.",
    ],
  }),

  methods: {
    login() {
      if (!this.$refs.login.validate()) {
        return;
      }

      if (this.$cookie.get(env.AUTH_COOKIE_NAME) != null) {
        this.setSnackbar("Already logged in.", "warning");
        return;
      }

      this.loading = true;

      this.$apollo
        .mutate({
          mutation: gql`
            mutation login($email: String!, $password: String!) {
              login(user: { email: $email, password: $password })
            }
          `,
          variables: {
            email: this.email,
            password: this.password,
          },
        })
        .then(({ data: { login } }) => {
          this.$cookie.set(env.AUTH_COOKIE_NAME, login, {
            expires: "30D",
            domain: env.COOKIE_DOMAIN,
          });
          this.setSnackbar("Succesfully logged in.", "success");
        })
        .catch((error) => {
          this.setSnackbar(error.message.split("GraphQL error:")[1], "error");
        })
        .finally(() => {
          this.loading = !this.loading;
          this.snackbar = false;
        });
    },
    setSnackbar(text, color) {
      this.status = text;
      this.statusColor = color;
      this.snackbar = true;
    },
  },
};
</script>

<style>
</style>