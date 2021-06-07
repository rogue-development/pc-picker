<template>
  <v-container class="d-flex justify-center align-center" fill-height>
    <v-container>
      <v-card>
        <v-card-text class="pa-0">
          <v-row>
            <v-col>
              <LoginForm />
            </v-col>
            <v-col v-if="!$vuetify.breakpoint.smAndDown" class="py-0 pl-0">
              <LoginDecoration />
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-container>
  </v-container>
</template>

<script>
import LoginForm from "@/components/Authentication/LoginForm.vue";
import LoginDecoration from "@/components/Authentication/LoginDecoration.vue";

export default {
  components: {
    LoginForm,
    LoginDecoration,
  },

  data: () => ({
    email: "",
    password: "",
    loading: true,

    emailRules: [
      (value) => !!value || "Email is required",
      (value) =>
        (!!value && value.match(/[^@ \t\r\n]+@[^@ \t\r\n]+\.[^@ \t\r\n]+/)) ||
        "Not a valid email",
    ],
    passwordRules: [
      (value) => !!value || "Username is required",
      (value) =>
        (!!value && value.length > 8) ||
        "Password must have atleast 8 characters.",
    ],
  }),
};
</script>

<style scoped>
</style>